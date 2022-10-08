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
## 
