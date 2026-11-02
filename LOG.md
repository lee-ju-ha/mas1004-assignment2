# Log

One entry for each recipe, selection or Track B model you train, newest at
the bottom. The numbers come from `experiments.csv`. "Why" and "what it means"
are in your own words: your agent asks you for them and does not make them up.
End the log with your plan for what to try next.

<!-- The form of an entry:

## <date> <tag> (Track A or B)
- changed: what is different from the run before
- why: your reason
- validation: 0.000 (before: 0.000)
- what it means: what you think the result says
-->

## 2026-10-30 baseline (Track A)
- changed: starter recipe unchanged; seeds 0 and 1
- why: starter photos를 확인하긴 했으나 몇 개의 사진만 보고 도시의 특징을 판단하여 recipe를 수정하는것은 무모하다고 생각했다. 그래서 우선 학습 후의 오답 사진을 통해 기준을 잡고 수정해나가는 것이 좋겠다고 생각했다.
- validation: seed 0 0.4984; seed 1 0.4957
- what it means: 도로 사진을 잘 구별하지 못한다. 사람이 지나다니는 길거리 사진을 잘 구별하지 못하며 특히 비오는날의 사진이 오답 사진에 많다.
- mistakes: 서울/부산 판단과 도쿄/오사카 판단이 잘 안된다고 생각해서 이를 개선해나가고 싶다. 서울/부산 오답 사진의 경우 지하철 역 사진은 부산, 궁궐 사진은 서울로 판단하는 경우가 많았다.
- next: 모든 도시의 오답 사진에서 길거리 사진이 많았기 때문에 각 도시의 길거리 특징을 찾아서 학습시키는게 좋을 것 같다.

## 2026-11-02 bottom_right_zoom (Track A)
- changed: 학습 사진의 오른쪽 아래 1/4을 잘라 224x224로 확대
- why: 도로 사진의 경우 도로표지판에 적힌 글자를 통해 어떤 도시인지 판단할 수 있다고 생각하여 위쪽을 가리면 모델이 어떻게 판단할지 궁금했다.
- validation: 0.4045 (baseline seed 0: 0.4984)
- what it means: 모델이 (일반적으로 위쪽에 존재하는) 도로표지판을 통해 도시를 판단할 것이라고 생각하였기 때문에 예상에 알맞은 결과가 나왔다.
- next: 아직 정하지 않음
