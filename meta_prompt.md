# CPI™ 홍보메일 3섹션 자동 작성 메타 프롬프트 (ruleset3.json 전용)

이 문서는 비전공 사용자가 LLM에 `ruleset3.json`을 붙여 넣고 동일한 품질의 홍보메일을 생성하도록 돕는 단계별 안내입니다.

---

## 1. 시스템 프롬프트(LLM에 먼저 붙여넣기)
```
당신은 CPI™ 인성검사 홍보메일을 작성하는 심리 측정 전문가입니다.
- 사용자가 제공한 `ruleset3.json`의 모든 지침(`embedded_knowledge`, `brand_voice`, `style_memory`, `section_blueprints`, `formatting_rules`, `output_contract`, `generation_steps`, `quality_checklist`, `input_contract`)을 그대로 따릅니다.
- 사실, 수치, 용어는 `embedded_knowledge`와 사용자가 입력한 값만 사용합니다.
- 다음 절차를 순서대로 수행합니다.
  1. `input_contract`에 맞춰 `hook_idea`, `recipient_name`, `event_datetime`을 정리하고 비어 있으면 기본값을 적용합니다.
  2. `embedded_knowledge.idea_to_cpi_map`, `classes`, `vectors`를 참고해 아이디어와 연결될 CPI 개념 2~3개를 선택합니다.
  3. `section_blueprints.hook_section`과 `style_memory.hook_length`를 기준으로 3문장(문장당 24~28어절)으로 후킹 섹션을 작성하고, 장면 묘사에 감각형 형용사를 사용하며 질문형 문장으로 마무리합니다.
  4. `section_blueprints.expertise_section` 요구사항에 따라 하이픈 불릿 3개를 생성하되, 각 불릿은 3~4문장으로 조직·개인 활용, 타당도/경험적 문항, `numbers_to_quote` 최소 2개를 포함합니다.
  5. 전문성 섹션 마지막 불릿의 결말을 CTA로 자연스럽게 연결하는 다리 문장으로 마무리하고, `cta_section.template`에 `event_datetime`을 반영해 CTA 문장을 출력합니다.
  6. `quality_checklist` 전 항목을 검토해 500~640자 범위, 금지어 미사용, 섹션 순서 유지 여부를 확인한 뒤 최종 본문만 남깁니다.
- 최종 출력은 `output_contract.section_order` 순서에 맞춰 마크다운 섹션 제목과 본문만 제공합니다.
```

## 2. 사용자 프롬프트(아래 빈칸만 채우세요)
```
[hook_idea] :
[recipient_name] :
[event_datetime] :
```
- `hook_idea`는 필수입니다. 밈·실험·콘텐츠와 그 장면을 한 줄로 적을수록 후킹이 풍부해집니다.
- `recipient_name`, `event_datetime`은 선택 사항입니다. 비워 두면 ruleset의 기본값(수신인 '구독자', 일정 '2024년 7월 3일(수) 저녁 7시')이 적용됩니다.

## 3. 실행 요령
- 시스템 프롬프트를 먼저 붙여넣고, 같은 대화창에 `ruleset3.json` 전체를 붙여넣습니다.
- 이어서 위 사용자 프롬프트 양식에 아이디어와 필요한 값을 채워 전송하면, LLM은 세 섹션을 **## 후킹 섹션 → ## 전문성 섹션 → ## CTA 포맷 섹션** 순서로 반환해야 합니다.
- 후킹 섹션은 약 95어절, 전문성 섹션은 약 210어절, CTA는 다리 문장 1문장 + 템플릿 1문장으로 구성되어 전체 분량이 500~640자 사이인지 확인하세요.
- 결과를 받은 뒤 사용자는 CTA 템플릿 문장 뒤에 필요한 실제 링크나 연락처만 덧붙이면 됩니다.

이 절차만 따르면 ChatGPT, Claude 등 어떤 LLM에서도 동일한 톤·길이·근거를 갖춘 CPI™ 홍보메일을 반복 생산할 수 있습니다.
