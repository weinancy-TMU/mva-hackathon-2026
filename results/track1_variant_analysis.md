# Track 1: BUB1B Variant Analysis

## 資料來源
- VCF: WGS_EX2312012_HGWCNDSX7.vcf.gz
- Reference: GRCh38 (no chr prefix)
- Variant caller: Sentieon Haplotyper + GATK VariantFiltration

## 候選致病變異（獨立分析）

### Allele 1: chr15:40209701 T>G
- Genotype: 0/1 (雜合)
- Depth: 46x (REF=21, ALT=25)
- GQ: 99 (最高品質)
- QUAL: 708.77
- FILTER: PASS
- dbSNP: 無 rsID（極稀有）
- MQ: 60（最高 mapping quality）

### Allele 2: chr15:40220612 T>G
- Genotype: 0/1 (雜合)
- Depth: 28x (REF=15, ALT=13)
- GQ: 99 (最高品質)
- QUAL: 344.77
- FILTER: PASS
- dbSNP: 無 rsID（極稀有）
- MQ: 60（最高 mapping quality）

## 重要限制
- 兩個變異距離 10,911 bp，短讀 WGS 無法確認 phase（trans/cis 未知）
- 需要 trio 資料或長讀定序確認 compound heterozygosity
- Allele 2 (40220612) 的蛋白質影響待 VEP 注釋確認（文獻報告為 p.Asn1002Lys，VUS）

## 下一步
- [ ] VEP 注釋確認蛋白質影響
- [ ] AlphaMissense 查詢 Allele 2 致病性
- [ ] 與 ClinVar 比對
