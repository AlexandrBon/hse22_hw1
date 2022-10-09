## Подготавливаю файлы для работы: 
```
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq 
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
```
## 5 миллионов рандомных чтений типа PE и 1.5 миллиона рандомных чтений типа MP:
```
seqtk sample -s1 oil_R1.fastq 5000000 > roil_R1.fastq
seqtk sample -s1 oil_R2.fastq 5000000 > roil_R2.fastq
seqtk sample -s1 oilMP_S4_L001_R1_001.fastq 1500000 > roilMP_S4_L001_R1_001.fastq
seqtk sample -s1 oilMP_S4_L001_R2_001.fastq 1500000 > roilMP_S4_L001_R2_001.fastq
```
## Оценка качества исходных чтений
```
mkdir fastqc
mkdir multiqc
ls r* | xargs -tI{} fastqc -o fastqc {}
multiqc -o multiqc fastqc
```
## Качество исходных чтений
![image](https://user-images.githubusercontent.com/66266655/194771155-481894fe-f38b-4fcc-9412-df57139dbb46.png)
![image](https://user-images.githubusercontent.com/66266655/194771160-501c1e87-667a-495b-8b77-1e930d02e28e.png)
![image](https://user-images.githubusercontent.com/66266655/194771176-1c0c2769-32ac-4753-ba9d-b6a254278e6a.png)
![image](https://user-images.githubusercontent.com/66266655/194771182-d9dfdb33-fdd4-41bd-aec4-85fba731d0b1.png)

## Подрезка значений, удаление адаптеров
```
platanus_trim roil_R*
platanus_internal_trim roilMP*
```
## Качество после подрезки
![image](https://user-images.githubusercontent.com/66266655/194772449-1809297e-e6c7-42a2-a6cc-72fd2c7fde59.png)
![image](https://user-images.githubusercontent.com/66266655/194772487-c737b0d5-d8d0-4313-b9fd-6607e5abca8f.png)
![image](https://user-images.githubusercontent.com/66266655/194772500-c8525abc-e4b0-40fe-9158-7c1bf832d8d8.png)
![image](https://user-images.githubusercontent.com/66266655/194772506-fcd526f3-77e5-44ac-ad8f-dce62d2510db.png)

## Cбор контигов и скаффолдов
```
platanus assemble -f roil_R1.fastq.trimmed roil_R2.fastq.trimmed
platanus scaffold -c out_contig.fa -IP1 roil_R1.fastq.trimmed roil_R2.fastq.trimmed -OP1 roilMP_S4_L001_R1_001.fastq.int_trimmed roilMP_S4_L001_R2_001.fastq.int_trimmed
```
## Уменьшаем кол-во гэпов с помощью подрезанных чтений
```
platanus gap_close -c out_scaffold.fa -IP1 roil_R1.fastq.trimmed roil_R2.fastq.trimmed -OP1 roilMP_S4_L001_R1_001.fastq.int_trimmed roilMP_S4_L001_R2_001.fastq.int_trimmed
```

Тут весь анализ: https://colab.research.google.com/drive/1w_Vhej2C6cwMCDh14Nt_4woa5qtmrb2s#scrollTo=aL5u24mGSkaj








