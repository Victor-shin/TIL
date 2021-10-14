# 1장 DDD를 시작하며


표1.4 비즈니스 최적의 모델 분석 

어떤 것이 비즈니스에 더 잘 맞는가?
서로 비슷해 보이는 두 번째와 세 번째 문장은 코드를 설계하는 방법에 차이가 있는가?

CASE1
- 가능한 관점
"그냥 코딩해버려. 누가 신경 쓴다고 그래?" -> 흠, 아예 틀렸군.
- 상응하는 코드 
patient.setShotType(ShotTypes.TYPE_FLU);
patient.setDose(dose);
patient.setNurse(nurse);

CASE2
- 가능한 관점
"환자에게 독감 주사를 놓는다." -> 좀 더 낫긴 하지만, 중요한 개념을 놓치고 있다.
- 상응하는 코드 
patient.giveFluShot();

CASE3
- 가능한 관점
"간호사가 환자에게 정량의 독감 백신을 투여한다." -> 적어도 더 배우기 전까지는 이 문장 정도로 일단 해보자.
- 상응하는 코드 
Vaccine vaccine = vaccine.standardAdultFluDose();
nerse.administerFluVaccine(patient, vaccine);


