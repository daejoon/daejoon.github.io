---
title: "EditorConfig 사용해보기"
categories: java
tags: editorconfig java intellij
---

# EditorConfig

> EditorConfig는 여러 개발자가 다양한 편집기와 IDE에서 동일한 프로젝트를 작업할 때 일관된 
> 코딩 스타일을 유지할 수 있도록 도와준다

* 추가적으로 IntelliJ는 `.editorconfig`의 확장 속성을 지원하기 때문에 팀원 모두가 IntelliJ를 사용한다면 코드의 통일성을 맞추기 쉽다.

## 코드

<script src="https://gist.github.com/daejoon/78fde4edef3b77dafcec520db3805f82.js"></script>

| 속성명                      | 뜻                               |
|--------------------------|---------------------------------|
| charset                  | 파일 인코딩 타입                       |
| insert_final_newline     | 파일이 줄바꿈으로 끝나야 하는지 여부            |
| end_of_line              | 줄의 끝 파일 형식                      |
| max_line_length          | 지정된 문자 수 뒤에 라인 줄 바꿈을 강제 적용      |
| ij_visual_guides         | intellij 전용 옵션, 코딩시 가이드 라인 문자 수 |
| indent_style             | 들여쓰기 스타일                        |
| indent_size              | 들여쓰기 크기                         |
| continuation_indent_size | 연속들여쓰기 코드블록과 연속줄 구분에 좋다         |
| trim_trailing_whitespace | 줄 끝에 공백을 제거할지 여부                |

## 참고

* [properties](https://github.com/editorconfig/editorconfig/wiki/EditorConfig-Properties)
* [intellij idea editorconfig](https://www.jetbrains.com/help/idea/editorconfig.html)