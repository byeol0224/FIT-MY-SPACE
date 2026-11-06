# 딱맞춤 상품 DB v0.1

목표: 다이소 300 / 무인양품 300 / 이케아 300 = 900개. **목표 수량은 실제 확보 수량이 아닙니다.**

초기 데이터는 제공된 `index.html`의 11개 항목을 추출했습니다. 최신 가격, 외경, 이미지 URL, 재고, 개별 상품 링크는 독립적으로 재검증하지 않았습니다. `verification_status=needs_reverification`이므로 운영용 검증 완료 데이터로 간주하지 마세요. `link_type=category`는 개별 상품이 아닌 카테고리 링크입니다. `image_status=url_unverified`는 사진 주소가 적혀 있을 뿐 실제 노출 여부를 확인하지 않았다는 뜻입니다.

파일: `fitmyspace.db` (SQLite), `fitmyspace_products.csv` (엑셀 편집용), `fitmyspace_products.json` (정적 웹 연결용).

추천용 승인 기준: 공식 개별 상품 링크, 상품명, 외경 3축, 대표 이미지 URL 확인 후 `verification_status=verified`, `image_status=verified`로 변경. 가격·재고는 별도 확인일을 기록하는 것이 좋습니다. 상품 식별자는 임시 내부 ID이며 쇼핑몰 상품번호가 아닙니다.

SQLite 치수 검색 예시 (cm):
```sql
SELECT * FROM products
WHERE verification_status='verified' AND image_status='verified'
AND height_cm <= 24
AND ((width_cm <= 39 AND depth_cm <= 29) OR (depth_cm <= 39 AND width_cm <= 29));
```

GitHub Pages는 SQLite를 브라우저에서 직접 읽지 않으므로 정적 사이트에서는 JSON을 fetch하거나 빌드 시 JS에 포함해야 합니다.
