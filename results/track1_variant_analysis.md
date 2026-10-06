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

## VEP 注釋結果（Ensembl VEP GRCh38, Jun2026）

### Allele 1: chr15:40209701 T>G → p.Leu737Ter (p.L737*)
- Consequence: stop_gained
- Gene: BUB1B (ENSG00000156970)
- Transcript: ENST00000287598.11 (canonical)
- Exon: 17/23
- Codon change: TTA→TGA
- 多個轉錄本顯示 NMD_transcript_variant → mRNA 預期被 NMD 降解
- 結論：功能喪失（Loss-of-Function），BUBR1 蛋白幾乎不產生

### Allele 2: chr15:40220612 T>G → p.Asn1002Lys (p.N1002K)
- Consequence: missense_variant
- Gene: BUB1B (ENSG00000156970)
- Transcript: ENST00000287598.11 (canonical)
- Exon: 23/23（最後一個 exon）
- Codon change: AAT→AAG
- 同時影響 PAK6 基因 intron（預計無功能影響）
- 結論：VUS（Variant of Uncertain Significance），需要 AlphaMissense 進一步評估

## 診斷結論
BUB1B compound heterozygous: p.Leu737Ter + p.Asn1002Lys
- 符合 MVA type 1 的分子診斷標準
- 重要限制：phase 未由短讀 WGS 確認（需 trio 或長讀定序）

## AlphaMissense 評估（Allele 2）

### p.Asn1002Lys
- AlphaMissense score: 0.923
- Class: likely_pathogenic（門檻 >0.564）
- 觀察：第 1002 位 Asn 幾乎所有替換都是 likely_pathogenic
  （除 p.Asn1002Ser = ambiguous 0.348）
- 意義：此位置高度保守，N1002 對 BUBR1 功能很重要
- 結論：p.Asn1002Lys 從 VUS 升級為 likely_pathogenic（計算預測層級）
- 重要限制：AlphaMissense 是計算預測，仍需實驗驗證確認功能影響

## gnomAD v4.1.2 驗證（2026-10-06）

### p.Asn1002Lys（15-40220612-T-G）
- Exomes: AC=1, AN=1,461,878, AF=6.841e-7
- Genomes: No variant
- Total AF: 6.195e-7
- Homozygotes: 0
- 只出現在 1 個 European non-Finnish XY 個體
- 來源：gnomAD v4.1.2（自行查詢確認，非 AI 推測）

## 重要更新：SLC34A1 p.Ala133Val（2026-10-06）

### Variant
- 位置：chr5:177386432 C>T（GRCh38）
- rsID：rs148976897
- 蛋白質影響：SLC34A1 p.Ala133Val（c.398C>T）
- Genotype：0/1（雜合），GQ=99，DP=49，AD=34,15，FILTER=PASS

### 為什麼 Ian 的 pipeline 沒有找到
- Ian 的 rarity cutoff：MAX_AF ≤ 0.001
- p.Ala133Val gnomAD AF ≈ 0.003（超過 cutoff）
- 在 early filter 就被排除，未進入 840 rare+impactful variants

### ClinVar 解讀
- 部分 submitter：Likely Pathogenic（nephrocalcinosis context）
- 部分 submitter：Likely Benign
- 結論：解讀有爭議，屬於 conflicting interpretations

### 目前定位
phenotype-matched candidate / possible modifier
不列入 Track 1 primary CSV
保留於 residual phenotype section（Track 2 報告）

### 重要科學意義
展示 hard AF cutoff 的限制：
pipeline threshold（AF>0.001）→ variant 被排除
→ phenotype-based rescue 發現潛在 relevant variant
→ HPO residual review 不是多餘的步驟
