# การกรอกข้อมูลสำหรับ Cancer Cohort

## แบบฟอร์ม
แบ่งเป็นสามแบบฟอร์มหลักที่เกี่ยวข้องกับโรคมะเร็ง **โดยให้กรอกแบบฟอร์มลงทะเบียนผู้ป่วยเข้าโครงการก่อน**
1. Cancer
1. Case Info - GDC
1. Diagnosis Info - GDC
1. Follow Up Info - GDC

## Cancer
- ข้อมูลเลขทะเบียนผู้ป่วย
- เก็บข้อมูลชนิดของมะเร็ง ด้วย ICD10
- Vital status ณ วันที่เก็บข้อมูล
- วันที่ตายและ สาเหตุการตาย

## Case Info
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
