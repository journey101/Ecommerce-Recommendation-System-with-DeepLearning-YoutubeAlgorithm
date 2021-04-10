## DS-CS2-Ecommerce-recommendation-system
ds-cs2-ecommerce-recommendation system development project adapting 'Youtube Recommendation algorithm'. 

### 1. 프로젝트 제목: 
- 뉴럴네트워크(딥러닝)를 활용한 이커머스 추천서비스 개발

### 2. 프로젝트 배경: 
- 식품군의 커머스 추천 모델에서 대부분의 커머스 서비스가 '빠른 배송', '특가/할인', '인기제품' 중심의 추천이 이뤄지고 있어 조금 더 개인화된 추천을 위해 사용자의 구매 정보를 바탕으로 '연관상품(ex. 우유+시리얼 조합추천)'이나 사용자의 평점 혹은 구매빈도가 높은 상품 등을 기준으로 추천하면 개인화된 추천서비스를 제공하여 소비자들의 만족을 높일 뿐 아니라, 구매를 더 촉진할 수 있을 것으로 예상하여 시작하게 되었다. 

- 커머스처럼 고객이 실시간으로 매우 많은 데이터를 양산하는 유튜브의 경우 특정 카테고리 영상(Ex.요리)을 본 다음, 요리영상만 시청하는 것이 아니라, 의식의 흐름대로 엔터테인먼트 영상을 보기도 한다. 커머스의 경우에도 특정 상품(ex. 화장품) 을 샀다가 키보드를 구매할 수도 있고, 유저 개인의 라이프스타일에 따라 구매했던 히스토리를 뉴럴네트워크(딥러닝)을 통해 학습하여 예측할 수 있다면 더 이상적인 커머스 플랫폼이 될 것이라는 기획의도로 본 프로젝트를 시작하게 되었다. 

### 3. 프로젝트 가설, 예상결과, 연관자료: 
<가설> 
 - 인스타카트 유저의 ‘재주문여부(reodered)’를 상품에 대한 평점(rating)으로 활용하여 like, dislike를 구분한 feature를 유튜브 추천방식인 ranking모델에 넣어 추출한 추천목록(1안)이 ‘주문회차(order_number)’를 평점(rating)개념으로 활용한 추천방식보다 추천목록(2안)의 평가지표인 nDCG 스코어가 높을 것이다. 

<예상결과>
 - (1안)의 추천목록 결과의 nDCG 수치가 (2안)에 비하여 더 높을 것이다. 
  - ※ recall, precision 대신 nDCG 를 비교하는 이유 : heavy 유저에 치중된 추천이 아니라, 신규 유저에게도 적합한 추천을 하기 위함이다. (cold-start문제 해소를 위한 방법) 

<연관자료>
 - 1.[[ 국내 이커머스 산업의 AI 활용현황과 전망 ] kdb미래전략연구소 산업기술리서치센터 보고서](https://file.mk.co.kr/meet/2020/06/pdf_readtop_2020_626590_1592459706.pdf) 

 - 2.[유튜브 추천모델 논문 (Deep Neural Networks for YouTube Recommendations)](https://static.googleusercontent.com/media/research.google.com/ko//pubs/archive/45530.pdf)

 - 3.[모델 성능 지표에 대한 참고 자료](https://medium.com/code-states/%EC%B6%94%EC%B2%9C-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-4e5044960bdd)

 - 4.[Learning to Rank와 nDCG 개념](https://yamalab.tistory.com/119)

 - 5.[Learning to Rank by Optimizing NDCG Measure](https://papers.nips.cc/paper/2009/file/b3967a0e938dc2a6340e258630febd5a-Paper.pdf)


### 4. 프로젝트 분석방법:
<분석방법>
 - (1) candidate generation model에서 후보목록을 추출한다. 
 - (2) 위 (1)의 모델을 활용하여 ranking model을 구축, 추천순위목록을 추출한다. 
  - (2-1) 추천순위 목록에 들어가는 rating feature를 아래 2가지 방법으로 진행한다. 
   - 방법1: 재주문(reordered) 여부 (1이면 like, 0이면 dislike) 
   - 방법2: 주문회차(order_number) (평균수치인 18번 이상이면 like, 18번 미만이면 dislike) 
 - (3) 방법 1, 2로 추출된 추천순위목록(ranking)의 ndcg 점수를 비교한다. 

<결론 및 인사이트> 
 - 방법 1,2를 nDCG지표로 비교하여 추천한다. 또한, 고객의 입장에서 구매 고려 시 정성적으로 어떤 의미가 있을지 추가적인 인사이트를 리포트하기로 한다. 

<분석환경>
 - 프로그래밍 언어: Python
 - 사용 라이브러리 및 패키지: Tensorflow, scikit-learn library
 - 분석환경: 구글 colab


### 5. 결과 요약 및 향후 보완하면 좋을 사항:

**<결과 요약>**

(1) ranking_2안의 결과가 nDCG 스코어에서 0.12 높았음.
 - ranking_1안 ndcg 평균: 0.35
 - ranking_2안 ndcg 평균: 0.47 

(2) ranking 1,2 안의 차이점:
  - (ranking_1안) reorder(재주문 여부)로 rating을 매긴 개념으로, 재주문을 한 경우(1)라면 **like**, 재주문을 안 한 경우(0)라면 **dislike**로 상품을 구분한 feature를 랭킹모델에 추가하여 추천목록을 생성한 방법. 
  - (ranking_2안) order_number(주문회차: 몇번째 구매인지)로 rating을 매긴 개념으로, 평균 주문회차인 18 이상인 경우(1) **like**, 18 미만(0)이면 **dislike**로 상품을 구분한 feature를 랭킹모델에 추가하여 추천목록을 생성한 방법. 

**<향후 보완하면 좋을 사항>**

(1) 마케팅 프로모션으로 발전시키기 
 - 본 추천목록으로 나온 상품목록 중 미구매 상품이라면, 프로모션 쿠폰을 제공하는 등 구매 촉진을 유도할 수 있을 것. 
 - 1, 2안에서 나온 추천목록 상품들로 다양한 마케팅적 A/B테스트가 가능할 것으로 보임. 

(2) 추천목록의 다양성 지표 보완하여 추천알고리즘 발전시키기
 - nDCG는 추천목록의 정확도 지표로 사용하며, 다양성 지표로서 "Entropy Diversity"가 있음. 
  - ※참고: https://yeomko.tistory.com/32
 - <참고자료 중에서 발췌>
  - Entropy Diversity란 이러한 엔트로피의 개념을 추천 결과에 적용한 것입니다. 모든 사용자들에게 비슷한 종류의 상품을 추천할 경우 해당 상품 추천은 자주 발생하므로 정보량이 낮습니다. 반면 개인에게 맞춤화 된 추천은 발생 횟수가 적으므로 정보량이 높아집니다. 이들의 기대값을 구한 것이 바로 Entropy Diversity입니다.
   - 5명의 유저에게 A부터 다섯개의 아이템 가운데 한개를 추천해주는 model A와 model B가 있다고 가정하겠습니다.  model A는 모든 유저에게 상품 A를 추천하였습니다. 이 경우 A가 추천될 확률은 1, 정보량은 0이 됩니다. 모든 유저대한 추천의 정보량이 0이므로 Entropy Diversity 역시 0이 됩니다. 반면 model B의 경우 모든 유저에게 각기 다른 상품을 추천합니다. 이 때 각각의 상품이 추천되는 확률은 0.2, 정보량은 0.32, 엔트로피는 1.6이 됩니다.

### 6. 프로젝트 작업자 (Collaborators)
 - 김현재 (hyeonjae.gim@gmail.com)
 - 오예은 (lovely.ohyeah@gmail.com)
 - 프로젝트 기획과정, 업무 일지: https://docs.google.com/spreadsheets/d/1F_dpeD6oU6LelSGLYVr_FeJeUvg6gxSp-WwDp1tY6zI/edit?usp=sharing
 
