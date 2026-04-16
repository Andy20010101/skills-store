# 1688 Supplier Discovery Report

## Research Brief
- Product direction: stainless steel insulated lunch box
- Search phrases used:
  - 保温饭盒
  - 不锈钢 保温 饭盒
  - 304 不锈钢 保温 便当盒
- Constraints:
  - price band: 15-35 RMB ex-factory reference
  - MOQ preference: <= 500 if possible
  - preferred supplier regions: Guangdong, Zhejiang
  - target materials: 304 stainless steel

## Run Notes
- Evidence mode: direct_1688
- Host capability assumptions: Hermes reused an operator-provided authenticated Chrome session exposed over CDP.
- Access limitations: no login or captcha blocker reappeared during the run, but direct search results were too thin or noisy to expand the run into a 3-supplier shortlist inside the iteration budget.
- Important caveats: this is a partial direct-site run with one credible supplier; automated login was not validated in this environment.

## Supplier Shortlist

### 1. 潮州市潮安区彩塘镇轩匠五金制品厂
- Evidence page link: https://shop07866986b0436.1688.com/?offerId=851436523899&td_page_id=PC-DEFAULT-2025
- Source 1688 link: https://shop07866986b0436.1688.com/?offerId=851436523899&td_page_id=PC-DEFAULT-2025
- Why shortlisted: supplier identity was clear on a direct 1688 shop page, and the linked 304 stainless-steel insulated lunch-box product stayed inside the target price and MOQ band for follow-up.

#### Page-Visible Facts
- 入驻2年
- 主营：餐具
- 店铺回头率：51%
- 店铺服务分：4.0分
- 准时发货率：96%
- 店铺好评率：99.0%
- 相关产品为 `304 不锈钢保温饭盒`
- visible capacities included `1.4L` and `1.6L`
- 新人价 `¥18.50 起`
- 首件预估到手价 `¥19.50 - ¥21.50`
- 起批：`1个`
- 已售：`20+个`

#### Heuristic Judgments
- the shop page and representative product page were both directly reachable in the authenticated session
- price and MOQ sat close to the requested sourcing band
- category fit was strong enough to keep this supplier as a credible follow-up candidate

#### Unknowns
- factory-direct status was not proven on the inspected pages
- certifications, export history, and production depth were not visible
- the run did not validate enough comparable suppliers to rank this candidate against a fuller set

#### Representative Products
1. 304不锈钢保温饭盒上班族便携带饭桶学生提锅便当盒汤壶碗
   - Evidence link: https://detail.1688.com/offer/851436523899.html?cosite=-&tracelog=p4p&_p_isad=1&clickid=55c752d094ad4fbe8038167439cb31f9&sessionid=c10c76944aa96f5cd0afae76266cb818
   - Source 1688 link: https://detail.1688.com/offer/851436523899.html?cosite=-&tracelog=p4p&_p_isad=1&clickid=55c752d094ad4fbe8038167439cb31f9&sessionid=c10c76944aa96f5cd0afae76266cb818
   - Visible price / MOQ: `¥18.50 起`; `1个起批`; 首件预估到手价 `¥19.50 - ¥21.50`
   - Notes: visible material claim `304不锈钢`; visible origin `潮州`; visible audience tags covered 儿童 / 学生 / 成人

## Rejected or Lower-Priority Candidates
- Candidate: additional direct search results under `保温饭盒`, `不锈钢 保温 饭盒`, and `304 不锈钢 保温 便当盒`
- Why not prioritized: the visible result set was too thin or noisy to validate more credible suppliers before Hermes hit its iteration cap

## Next Actions
- Which suppliers to revisit first: 潮州市潮安区彩塘镇轩匠五金制品厂
- Which unknowns need manual confirmation:
  - whether the supplier is factory-direct
  - certification, lead time, and export experience
  - whether two additional direct 1688 suppliers can be validated in the same authenticated workflow
