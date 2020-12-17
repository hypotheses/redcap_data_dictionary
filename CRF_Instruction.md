# การกรอกข้อมูลสำหรับ Cancer Cohort

## แบบฟอร์ม
แบ่งเป็น 5 แบบฟอร์มหลักที่เกี่ยวข้องกับโรคมะเร็ง **โดยให้กรอกแบบฟอร์มลงทะเบียนผู้ป่วยเข้าโครงการก่อน**
น้อยที่สุดที่ต้องกรอกคือ form "Minimal Cancer Registry Information" 

1. Minimal Cancer Registry Information
1. Cancer
1. Case Info - GDC
1. Diagnosis Info - GDC
1. Follow Up Info - GDC

## Minimal Cancer Registry Information (Form Name: Cancer)
- ICD-10 
- Vital Status: Death/Alive
  - Date of death
  - Cause of death
- TNM Cancer staging
- Last known status: tumor free/with tumor/distant|local metastasis/recurrence/progression
- Date of last known status
- Evidence of progression
- Treatment received
- Best improvement from the treatment
- Treatment regimens: dose/cycle
- Detail of the radiation

## Additional Cancer Registry Information (Form Name: Case Info)
- ข้อมูลเลขทะเบียนผู้ป่วย
- ชนิดของการได้รับ consent 
- ระยะเวลาจากวันที่ได้รับการวินิจฉัย (indexed date) จนถึงวันที่เข้าร่วมโครงการ
- ระยะเวลาจากวันที่ได้รับการวินิจฉัย (indexed date) จนถึงวันที่ผู้ป่วย lost to follow-up
- วันที่ได้รับการวินิจฉัยโรค (indexed date)
- สถานะในการ Follow up และ วันสุดท้ายของการ Follow up

## Diagnosis Info
- HN
- วันที่ได้รับ pathological diagnosis
- ICD-O histology description (free text)
- ICD-O Anatomical site (free text)
- Date used for indexed and the date for diagnosed with the malignant disease
- อายุที่ได้รับการวินิจฉัย (หน่วยเป็นวัน)
- อายุ (คำนวณเป็นปี) สำหรับ obfuscation
- ที่มาของชิ้นเนื้อมะเร็ง (primary/metastasis/recurrence/unknown)
- ICD-O code

## Follow Up Info
- source ของข้อมูลสาเหตุการตาย
