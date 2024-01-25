# メトリクス
（テーマ：古典的なメトリクスベースの臭い検出．JDTParser程度のツールから得られる範囲で．）

### M0. 与えられたソースファイルを構文解析せよ．

### M1. 与えられたプロジェクトディレクトリに含まれる全ソースファイルを解析し，すべてのクラス/モジュール$`C`$，メソッド/関数$`M`$，フィールド/属性$`F`$を列挙せよ．

### M2. 与えられたメソッドの[循環的複雑度](https://ja.wikipedia.org/wiki/循環的複雑度)（サイクロマチック複雑度; Cyclomatic complexity）を計測せよ．
- T.J. McCabe: "[A Complexity Measure](http://www.literateprogramming.com/mccabe.pdf)". IEEE Trans. Softw. Eng. SE-2(4) 308-320, 1976. DOI:[10.1109/TSE.1976.233837](https://doi.org/10.1109/TSE.1976.233837)

### M3. 与えられたクラスの WMC（Weighted Methods per Class）を計測せよ．
WMC はクラスに所属するメソッドの複雑さ重みの和として計算される．
メソッドの複雑さ重みには循環的複雑度を用いよ．
- S.R. Chidamber , C.F. Kemerer: "[A Metrics Suite for Object Oriented Design](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)". IEEE Trans. Softw. Eng. 20(6) 476-493, 1994. DOI:[10.1109/32.295895](https://doi.org/10.1109/32.295895)
- [Object-Oriented Metrics in Practice](https://doi.org/10.1007/3-540-39538-5)による定義:
  "The sum of the statical complexity of all methods of a class. The CYCLO metric is used to quantify the method’s complexity"

### M4. メソッドと，メソッドが使用するフィールドの間のUse関係$`\to_u: M \times F`$を抽出せよ．

### M5. 与えられたメソッドがアクセサメソッド（getter/setter）かどうか判定せよ．

### M6. メソッド間の呼び出し関係$`\to_c: M \times M`$を抽出せよ．

### M7. 与えられたクラスのATFD（Access To Foreign Data）を計測せよ．
ATFDは，対象クラスから（アクセサメソッドによる間接アクセスも含めて）アクセスしている外部クラスのフィールド数を表す．
- [Object-Oriented Metrics in Practice](https://doi.org/10.1007/3-540-39538-5)による定義:
  "The number of attributes from unrelated classes that are accessed directly or by invoking accessor methods"

### M8. 与えられたクラスの TCC（Tight Class Cohesion）を計測せよ．
TCCは凝集度のメトリクスのひとつで，対象クラス内のすべてのメソッド対のうち，同クラスの特定のフィールドに共通してアクセスするものの割合を表す．
- [Object-Oriented Metrics in Practice](https://doi.org/10.1007/3-540-39538-5)による定義：
  "The relative number of method pairs of a class that access in common at least one attribute of the measured class"

### M9. 与えられたクラスが不吉な臭いGod Classを持つかを判定せよ．
[Object-Oriented Metrics in Practice](https://doi.org/10.1007/3-540-39538-5)によるメトリクスベースの判定戦略によれば，下記を条件をすべて満たすクラスをGod Classとみなす．
- `ATFD > FEW` (= 5) (Class uses directly more than a few attributes of other classes)
- `WMC >= VERY HIGH` (= 47) [% (Functional complexity of the class is very high)
- `TCC < 1/3` (Class cohesion is low)

閾値には`FEW = 5`, `VERY HIGH = 47`を用いよ．
静的解析ツール[PMD](https://pmd.github.io/)による検出も試み，結果を比較せよ．
