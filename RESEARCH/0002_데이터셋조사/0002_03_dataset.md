**출처 정보 (Source Info)**: `datasets` 내 8개 데이터셋의 실제 파일 컬럼명, `data_dictionaries` 폴더 내 Excel 딕셔너리 명세서, `pdfs` 폴더 내 프로토콜 참조.

각 데이터셋 별로 데이터 분류(G, Q, M, I, A, S)에 해당하는 **실제 원문 컬럼명(Original Column Names)** 을 매핑하여 기재하였습니다. 발견되지 않은 항목(X)의 경우 해당 범주의 수집 변수가 없는 것으로 파악됩니다.

> 수정 이력: 원본 보고서 대비 검증을 통해 "컬럼명 오류", "O/X 판정 오류", "데이터셋 간 변수 혼동" 등을 수정하였습니다.

---

## 1. AIDET1D (AIDET1D_Data_Tables)

| 카테고리 | 포함여부 | 원문 컬럼명 (Original Column Names) |
| :---: | :---: | :--- |
| **G** (CGM) | O | `GlucValue` (AIDEDeviceCGM), `glucValue` (cgmAnalysis), `gluMean`, `gluAbove180`, `gluBelow70` (gluIndices), `SensorGluc` (AIDEDiabDKAEvent/HypoEvent), `CGMUseDevice` (AIDEDiabScreening), `currentGlucoseDisplayValue` (AIDETandemCGMDATAGXB) |
| **Q** (Survey) | O | `AgeAsofEnrollDt` (PtRoster), `Sex`, `Race`, `Ethnicity` (AIDEDiabScreening), `Weight`, `Height` (AIDEDiabPhysExam), `T1DDuration1Yr` (AIDEEligSrcDataCapt), `AnnualIncome`, `EducationLevel` (AIDEDiabSocioEcon) |
| **M** (Clinical) | O | `HbA1cTestRes` (AIDEDiabLocalHbA1c), `BUN`, `KetoneSerum`, `KetoneUrine` (AIDEDiabDKAEvent), `BldPrSys`, `BldPrDia`, `Temp` (AIDEDiabPhysExam) |
| **I** (Insulin/Carb) | O | `UnitsInsTotal`, `NumPumpBolusOrShortAct`, `InsModPump`, `PumpType` (AIDEDiabScreening/Treatment), `BasalBolusRegimen`, `CarbRatioMealBol` (AIDEEligSrcDataCapt), `InsulinName`, `InsRoute` (AIDEInsulin) |
| **A** (Activity) | X | 웨어러블/활동 추적기 데이터 없음. `PEHeartRt`는 신체검사(Physical Exam) 심박으로 활동 추적 아님 |
| **S** (Self-Report/App) | △ | 임상 설문 다수 존재: BDEFS, HypoFear, TechAccept, SystemUsability 등 (Q1~Q40 형식). 단, 기준 정의("사용자 로그: 식사, 운동, 약물 복용")에 정확히 부합하는 자가 보고 데이터(식사일지, 운동기록 등)는 부재 |

## 2. Bangladeshi Patients T2 (Bangladeshi_Patients_T2_Dataset)
| 카테고리 | 포함여부 | 원문 컬럼명 (Original Column Names) |
| :---: | :---: | :--- |
| **G** (CGM) | X | `Glucose`는 단일 혈당 측정치이며 연속혈당(CGM) 아님 |
| **Q** (Survey) | O | `Age`, `BMI` |
| **M** (Clinical) | O | `Glucose`, `BP(Systolic)`, `BP(Diastolic)`, `Skin Thickness(mm)`, `No. of Pregnancy`, `DiabetesPedigreeFunction` |
| **I** (Insulin/Carb) | O | `Insulin` (단일 지표) |
| **A** (Activity) | X | 해당 없음 |
| **S** (Self-Report/App) | X | 해당 없음 |

## 3. CGMND (CGMND_Data_Tables)
| 카테고리 | 포함여부 | 원문 컬럼명 (Original Column Names) |
| :---: | :---: | :--- |
| **G** (CGM) | O | `Value` (CGMNDDeviceCGM — 연속 혈당 수치), `DeviceDtTm` (측정 타임스탬프), `Sensor_Location` (CGMNDScreening) |
| **Q** (Survey) | O | `Age`, `Gender`, `Race`, `Ethnicity`, `BMI`, `Height_cm`, `Weight_kg` (CGMNDScreening) |
| **M** (Clinical) | O | `Hba1cValue`, `GAD65Value`, `ZnT8Value`, `IA2Value`, `IAAValue` (CGMNDTestResults), `Hba1c_POC` (CGMNDScreening) |
| **I** (Insulin/Carb) | X | 비당뇨 소아 대상이므로 인슐린 투여 기록 부재 |
| **A** (Activity) | O | `Nap_SleepTime`, `Sleep_Time`, `Wake_Time`, `Nap_WakeTime` (CGMNDSleepWakeLog) |
| **S** (Self-Report/App) | X | `Med1`~`Med3`는 스크리닝 시 연구자가 기록한 기존 복용 약물 목록이며, `AE_Description`은 연구자 작성 이상반응 보고로, 환자 자가 보고 로그가 아님 |

## 4. GLAM (GLAM_Data_Tables)
| 카테고리 | 포함여부 | 원문 컬럼명 (Original Column Names) |
| :---: | :---: | :--- |
| **G** (CGM) | O | `Value` (tblGLAMDeviceCGM — 연속 혈당 수치), `DeviceDtTm` (타임스탬프), `CGMInsDt` (GLAMCGMInsertion — 센서 삽입일), `CGMDisconDt` (GLAMCGMRelatedAE — 센서 제거일). 참고: `OGTTCGM`(GLAMOGTT)은 OGTT 시 CGM 착용 여부 플래그 |
| **Q** (Survey) | O | `AgeAsofEnrollDt` (PtRoster), `Ethnicity`, `Race`, `EducationLevel` (GLAMCompEnrollment), `Weight`, `Height` (GLAMCompEnrollment), `GestAgeWks` (GLAMUltrasoundResults). 참고: `Sex`는 GLAMPostDelivery에 있으나 신생아 성별임 |
| **M** (Clinical) | O | `HbA1cResults` (GLAMCompEnrollment), `HbA1cTestRes` (GLAMHbA1cResults), `Hr0Result`, `Hr1Result`, `Hr2Result`, `Hr3Result` (GLAMOGTT — OGTT 결과), `BldPrSys`, `BldPrDia` (GLAMOGTT/GLAMCompEnrollment), `GDMDiag` (GLAMPostDelivery) |
| **I** (Insulin/Carb) | △ | `GDMInsulin` (GLAMCompEnrollment — GDM 인슐린 사용 이력 Yes/No 플래그), `GDMTrtInsulin` (GLAMPostDelivery — 치료 인슐린 사용 플래그), `PCOSMed` (GLAMCompEnrollment). 실제 인슐린 투여량 데이터는 부재, 탄수화물 섭취 입력량도 부재 |
| **A** (Activity) | X | `FetalHR`(GLAMUltrasoundResults)는 초음파로 측정한 태아 심박수이며, 참가자(산모)의 활동 추적기/웨어러블 데이터 아님 |
| **S** (Self-Report/App) | O | `LogMeals` (GLAMCompEnrollment — 식사 기록 여부), `MealDateTime` (GLAMMealLog — 식사 시간 로그) |

## 5. IOBP2 (IOBP2_Data_Tables)
| 카테고리 | 포함여부 | 원문 컬럼명 (Original Column Names) |
| :---: | :---: | :--- |
| **G** (CGM) | O | `CGMVal` (IOBP2DeviceiLet), `Value` (IOBP2DeviceCGM), `SensorGluc` (IOBP2DiabDKAEvent/HypoEvent), `CGMType` (IOBP2RandBaseInfo), `GlucValue` (IOBP2DeviceCGMAlertSet) |
| **Q** (Survey) | O | `AgeAsofEnrollDt` (IOBP2PtRoster), `Sex`, `Race`, `Ethnicity` (IOBP2DiabScreening), `Weight`, `Height` (IOBP2HeightWeight), `AnnualIncome`, `EducationLevel` (IOBP2DiabSocioEcon) |
| **M** (Clinical) | O | `HbA1cTestRes` (IOBP2DiabLocalHbA1c), `BUN` (IOBP2DiabDKAEvent), `KetoneVal` (IOBP2DeviceKetone), `KetoneSerum` (IOBP2DiabDKAEvent), `EGFRResult` (IOBP2eGFR) |
| **I** (Insulin/Carb) | O | `TotDlyIns` (IOBP2RandBaseInfo), `BasRtChgNewRt` (IOBP2BasalRtChg), `MealBolus`, `MealSize` (IOBP2DeviceiLet — 탄수화물 양), `PumpType` (IOBP2DiabScreening), `InsInjAmt` (IOBP2ManualInsulinInj) |
| **A** (Activity) | X | 웨어러블/활동 추적기 데이터 없음. `BPUOSSleepTrouble`은 BPUOS 설문 문항, `EQ5D5LMobility`는 삶의 질 설문 문항으로, 활동 추적기 데이터가 아님 |
| **S** (Self-Report/App) | O | `MealDoseType`, `MealDoseAnnounceTm`, `MealDoseAnnounceAmt` (IOBP2MealDose — 식사 시 기록), `DlySurvLowBG`, `DlySurvLowBGCarbGrams` (IOBP2PSTransDailyQuest — 일일 설문), 다수 자가 설문: HFS, PAID, DTSQ, Clarke, BPUOS, T1DDS, WHO-5 등 |

## 6. PEDAP (PEDAP_Data_Files)
| 카테고리 | 포함여부 | 원문 컬럼명 (Original Column Names) |
| :---: | :---: | :--- |
| **G** (CGM) | O | `CGMValue` (PEDAPTandemCGMDATAGXB), `CGM` (PEDAPDexcomClarityCGM), `CalibrationValue` (PEDAPDexcomClarityCalibration), `SensorGluc` (PEDAPDiabDKAEvent/HypoEvent) |
| **Q** (Survey) | O | `AgeAsofEnrollDt` (PtRoster), `Sex`, `Race`, `Ethnicity` (PEDAPDiabScreening), `Weight`, `Height` (PEDAPDiabPhysExam), `WaistCirc` (PEDAPDiabPhysExam), `AnnualIncome`, `EducationLevel` (PEDAPDiabSocioEcon) |
| **M** (Clinical) | O | `HbA1cTestRes` (PEDAPScreeningCTV), `BUN`, `KetoneSerum` (PEDAPDiabDKAEvent), `BldPrSys`, `BldPrDia`, `PEHeartRt`, `FingStkBG` (PEDAPDiabPhysExam), `Ketone` (PEDAPKetone) |
| **I** (Insulin/Carb) | O | `InsBasal0000`~`InsBasal2330` (PEDAP InsulinDeliveryDetails — 시간대별 기저량), `BolusAmount`, `CarbAmount` (PEDAPTandemBolusDelivered), `PumpTotInsDaily` (PEDAPInsulinDeliveryDetails), `BasalRate` (PEDAPTandemBASALDELIVERY) |
| **A** (Activity) | △ | 웨어러블/활동 추적기 기기 데이터는 없으나, 수면 설문 존재: `PSQIParentActualSleepHours`, `PSQIParentBedtimeHr`, `PSQIParentSleepQuality` (PEDAPPSPSQIParent). `PEHeartRt`는 신체검사 심박(임상 측정) |
| **S** (Self-Report/App) | O | `MealCarbs` (식사 탄수화물), `ExerciseStartHr`, `ExerciseEndHr` (운동 시작/종료) (PEDAPMealExerciseLog), 다수 부모 설문: HypoFear, HypoConf, PedsQL, PedInv, SystemUsability, INSP 등 |

## 7. Shanghai T1DM (Shanghai_T1DM)
| 카테고리 | 포함여부 | 원문 컬럼명 (Original Column Names) |
| :---: | :---: | :--- |
| **G** (CGM) | O | `CGM (mg / dl)` |
| **Q** (Survey) | X | 인구통계/설문 데이터 없음 (환자별 개별 시계열 파일만 존재) |
| **M** (Clinical) | O | `Blood Ketone (mmol / L)`, `CBG (mg / dl)`, `Non-insulin hypoglycemic agents` |
| **I** (Insulin/Carb) | O | `CSII - basal insulin (Novolin R, IU / H)`, `CSII - bolus insulin (Novolin R, IU)`, `Insulin dose - i.v.`, `Insulin dose - s.c.` |
| **A** (Activity) | X | 해당 없음 |
| **S** (Self-Report/App) | O | `Dietary intake`, `饮食` (식사 기록) |

## 8. Shanghai T2DM (Shanghai_T2DM)
| 카테고리 | 포함여부 | 원문 컬럼명 (Original Column Names) |
| :---: | :---: | :--- |
| **G** (CGM) | O | `CGM (mg / dl)` (일부 파일에서 `CGM`으로 축약) |
| **Q** (Survey) | X | 인구통계/설문 데이터 없음 |
| **M** (Clinical) | O | `Blood Ketone (mmol / L)` (일부: `Blood Ketone`), `CBG (mg / dl)` (일부: `CBG`), `Non-insulin hypoglycemic agents` |
| **I** (Insulin/Carb) | O | `CSII - basal insulin (Novolin R, IU / H)`, `CSII - bolus insulin (Novolin R, IU)`, `Insulin dose - i.v.`, `Insulin dose - s.c.`, 변형: `胰岛素泵基础量 (Novolin R, IU / H)`, `CSII - bolus insulin (Novolin R  IU)` (쉼표 누락) |
| **A** (Activity) | X | 해당 없음 |
| **S** (Self-Report/App) | O | `Dietary intake`, `饮食` (일부 파일: `进食量`) |

---

## 범례
- **O**: 해당 카테고리 변수 존재
- **X**: 해당 카테고리 변수 없음
- **△**: 관련 변수가 존재하나 기준 정의와 완전히 부합하지 않는 경우 (제한적 포함)



---

논문(Glucose-ML)의 주요 데이터 처리 및 샘플링 기준
디바이스별 원본 샘플링 주파수 유지 (Raw Frequency)

논문은 각 CGM 기기의 고유한 데이터 수집 주기를 그대로 존중합니다.
Dexcom 및 Medtronic CGM: 약 5분 간격(every 5 minutes)으로 1개의 데이터 샘플.
Abbott FreeStyle Libre CGM: 약 15분 간격(every 15 minutes)으로 1개의 데이터 샘플.
예측 모델(단순 선형 회귀 등)을 만들 때도 5분 간격 기기는 과거 10분 치, 15분 간격 기기는 과거 30분 치를 사용하여 분석 파라미터를 동적으로 조정했습니다. (데이터 강제 다운샘플링 안 함)
결측치 보간(Interpolation) 금지

논문 452행 및 584행 등에서 명시적으로 언급합니다.
"결측치가 있는 구간을 보간법(Interpolation)이나 외삽법(Extrapolation)으로 채우지 않고 분석에서 아예 제외(Exclude)했습니다. 왜냐하면 이렇게 채워넣은 데이터에서 모델을 평가하면 오류가 유입되어 정확도를 신뢰할 수 없게 되기 때문입니다."
즉 빈 공간을 평균이나 선형 이어그리기로 채우지 않고, 누락된 채로(Missing) 남겨두고 평가합니다.
결측 구간 판별 최소 기준 설정

특정 기기의 기본 수집 주기에 3배의 시간이 지나도 데이터가 없으면 '결측(Missing data)'으로 간주했습니다.
예) 5분 간격 측정(Dexcom)의 경우: 15분 이상 데이터가 기록되지 않으면 해당 구간은 누락 구간으로 처리.
현실적이지 않은 값 제거 (Data Cleaning)

혈당 40~400 mg/dL 범위를 벗어난 값이나 "LOW", "HIGH" 등의 텍스트 제거.
변화율이 너무 빠른 경우(예: 1분에 20mg/dL 초과)는 센서 오류로 간주하여 필터링.
