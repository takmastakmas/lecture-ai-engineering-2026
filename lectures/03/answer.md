# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：第1回では文章としては正しいが、本講座の内容ではない回答であったが、今回は本講座の内容に沿った回答になった。
- `--trace` で見えたツール呼び出し（ツール名と引数）：
[tool call]   search_glossary({'query': 'LoRA'})
[tool call]   search_glossary({'query': 'QLoRA'})
- 1つの質問での LLM 呼び出し回数（`requests`）：requests=2
- 追加したツールと、docstring に書いた説明：
def make_quiz(lecture: int) -> str:
    """指定した回（1始まりの整数）の講義に関する確認問題を1問返す。

    「第2回の確認問題を出して」のように頼まれたときに使う。第N回の用語一覧から1つをランダムに選び、
    問題と答えを JSON で返す。モデルはこの結果をそのまま出題文に使う。
    """

## 宿題

- 取り組んだレベル：基礎
- やったこと：search_glossary の docstring の「query には調べたい用語を1つだけ入れる」を「まとめて入れる」に変える
- 結果：
[tool call]   search_glossary({'query': 'LoRA, QLoRA'})
変更前
[usage] RunUsage(cost=Decimal('0.0008488'), details={'text_prompt_tokens': 1196}, input_text_tokens=1196, input_tokens=1196, output_tokens=196, requests=2, tool_calls=2)
変更後
[usage] RunUsage(cost=Decimal('0.0008546'), details={'text_prompt_tokens': 1132}, input_text_tokens=1132, input_tokens=1132, output_tokens=206, requests=2, tool_calls=1)
- 気づき・疑問：
tool callは予想どおり2回から1回になった。回答の質やtoken数にはあまり変化はなかった。調べたいか調べたくないかはどうやって判断しているのか？