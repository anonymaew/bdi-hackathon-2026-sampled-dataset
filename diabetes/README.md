---
title: "ชุดข้อมูล EMR ผู้ป่วยเบาหวานแบบติดตามยาว"
track: "Health"
domain:
  - "Clinical"
  - "Diabetes Research"
source:
  - "โรงพยาบาลศรีนครินทร์ มหาวิทยาลัยขอนแก่น"
total_records: 70000
sampled_records: 100
filetype:
  - "xlsx"

---

# ชุดข้อมูล EMR ผู้ป่วยเบาหวานแบบติดตามยาว

## คำอธิบาย
ชุดข้อมูลผู้ป่วยโรคเบาหวานจาก EMR จำนวนรวมประมาณ **70,000 คน** (ตัวอย่าง **100 คน**) แบ่งเป็น:
- **เบาหวานประเภท 1 (Type 1)**: ประมาณ 2,000 คน
- **เบาหวานประเภท 2 (Type 2)**: ประมาณ 50,000 คน
- **เบาหวานที่ไม่ทราบประเภท (Unknown)**: ประมาณ 20,000 คน

ข้อมูลบันทึกตลอดช่วงเวลา โดยแบ่งเป็น Periods (ช่วงละ 60 วัน) รอบวันที่วินิจฉัยโรค (baseline / `dm_onset`)

## ฟิลด์ข้อมูล

### ข้อมูลผู้ป่วย
| ฟิลด์ | คำอธิบาย |
|-------|----------|
| `age` | อายุผู้ป่วย ณ วันที่ baseline |
| `sex` | เพศ (`FEMALE` / `MALE`) |
| `identify_by` | วิธีการระบุเข้า dataset (`medication`, `icd10`, `lab`) |
| `dm_onset` | วันที่วินิจฉัยโรคเบาหวาน (baseline) |
| `type1` / `type2` / `gdm` | ตัวบ่งชี้ประเภทเบาหวาน (0/1) |

### ค่าสัญญาณชีพ (Vitalsign): ตาม Period P
สัญญาณชีพ เช่น `resp`, `o2sat`, `temp`, `hr`, `ht`, `wt`, `bmi`, `sbp`, `dbp`

### ค่าห้องปฏิบัติการ (Lab): ตาม Period P
เช่น `fpg`, `hba1c`, `cpeptide`, `wbc`, `platelet`, `hemoglobin`, `lipid profile`, `thyroid`, `troponin`, `proBNP` ฯลฯ

### โรคประจำตัว (Comorbidity): ตาม Period P
เช่น `arrhythmias`, `atrial_fibrillation`, `cad`, `dementia`, `hf`, `stroke`, `ht`, `ckd`

### ยาที่ใช้ (Medication): ตาม Period P
เช่น `metformin`, `insulin`, `dapagliflozin`, `semaglutide`, `sitagliptin` ฯลฯ

### Period P
- **P = -1** : ก่อน dm_onset 30-90 วัน
- **P = 0** : ก่อนและหลัง dm_onset 30 วัน
- **P = 1** : 30-90 วันหลัง dm_onset
- ค่า P อื่นๆ เป็นช่วง 60 วัน

## โครงสร้างไฟล์
| ไฟล์ | รูปแบบ |
|------|--------|
| [`data_dictionary_diabetes_example.xlsx`](data_dictionary_diabetes_example.xlsx) | Excel (Data Dictionary) |

## โจทย์ / แนวทางวิเคราะห์
- **Type Classification**: จำแนกประเภทเบาหวาน (Type 1 vs Type 2)
- **Risk Stratification**: ประเมินความเสี่ยงภาวะแทรกซ้อน (หัวใจ, ไต, สมอง)
- **Treatment Recommendation**: แนะนำแนวทางการรักษา
- **Predictive Model**: พยากรณ์ผลลัพธ์ทางคลินิก (HbA1c, ภาวะแทรกซ้อน)
- **Medication Effectiveness**: ประสิทธิภาพของยารักษาเบาหวาน
- **Trend Analysis**: ติดตามแนวโน้มค่า Lab/Vitalsign ตามเวลา

## หมายเหตุ
- ข้อมูลมีฟิลด์แบบ longitudinal (ตาม Period P)
