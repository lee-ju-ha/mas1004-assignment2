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

## 2026-11-03 grayscale (Track A)
- changed: 오른쪽 아래 확대를 빼고, 학습 사진을 흑백으로 변환
- why: 상대적으로 색채가 화려한 도시가 있기 때문에 도시마다의 차이를 줄여서 비교해보고 싶었다.
- validation: 0.4274 (baseline seed 0: 0.4984; bottom_right_zoom: 0.4045)
- what it means: 도시의 색채가 모델의 판단에 영향을 미친다는 것을 알게 되었다.
- next: 사진을 좌우반전하고 싶다.

## 2026-11-03 balanced (Track A)
- changed: 모든 사진은 유지하고, 도시별 샘플링 비중을 같게 조정
- why: 부산이랑 도쿄, 서울의 사진 수가 2배 이상 차이 나기 때문에 모델 학습에 영향을 미칠 것이라 생각하였다.
- validation: 0.5092 (baseline seed 0: 0.4984); Busan 0.4561 (baseline seed 0: 0.3748)
- what it means: 부산 data 수가 적어서 부산 점수 또한 낮게 나온다고 생각했고, 도시별 비중을 동일하게 한 결과 유의미하게 점수가 올라서 각 도시의 사진 수가 모델 학습에 영향을 미친다는 사실을 알게 되었다.
- next: 아직 정하지 않음

## 2026-11-03 always_flip (Track A)
- changed: 학습 사진에 무작위 좌우반전 대신 항상 좌우반전을 적용; 도시별 샘플링 균형 조정은 사용하지 않음
- why: 도로에서 나타나는 도시별 특징인 (서울, 부산, 타이베이 우측통행 / 도쿄, 오사카 좌측통행) 차량의 통행 방향이 모델 학습에 미치는 영향을 알아보고 싶다.
- validation: 0.4856 (baseline seed 0: 0.4984)
- what it means: baseline보다 낮은 점수가 나온 것을 통해 좌우반전이 모델의 학습에 유의미한 도움을 주지 않았다고 생각한다.
- next: 실내 사진을 제외하고 학습을 진행하고 싶어.

## 2026-11-04 balanced_always_flip (Track A)
- changed: 도시별 균형 샘플링과 항상 좌우반전을 함께 적용
- why: 시도했던 실험 중에 점수가 높게 나왔기 때문이다.
- validation: 0.4958 (balanced: 0.5092; always_flip: 0.4856)
- what it means: 둘의 시너지가 생겨 점수 상승을 기대했으나 높게 나오지 않았다.
- next: 아직 정하지 않음

## 2026-11-05 balanced_wd01 (Track A)
- changed: balanced 샘플링을 유지하고 weight decay를 0.05에서 0.1로 변경
- why: 리더보드에서 다른 학생들의 weight decay 0.1 실험을 봤고, 아직 시도하지 않은 설정이라 점수가 높았던 balanced와 결합해 점수가 오르는지 확인하고 싶었다.
- validation: 0.5039 (balanced: 0.5092; baseline: 0.4984)
- what it means: baseline보다 높은 점수가 나왔기 때문에 모델 학습에 도움을 준 것으로 확인할 수 있다.
- next: 아직 정하지 않음
