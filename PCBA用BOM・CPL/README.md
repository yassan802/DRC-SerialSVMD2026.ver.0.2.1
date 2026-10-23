2026年10月23日更新。DRC-SerialSVMD2026.ver.0.2.1の同日16:46:52保存PCBから生成したJLCPCB用BOM・CPL。

アップロードするファイルは **bom.csv** と **positions.csv**。BOMは1枚分、CPLも単板1枚分である。基板製造5枚・PCBA 2枚は注文画面で指定する。BOMの数量を2倍にしない。

PCBA対象は13品番・18点／枚、2枚合計36点。すべてF面（top）。CH340Eは秋月購入・手はんだとして除外し、表面のみのPCBA構成を維持した。Gerber・ドリルは今回の更新対象外。

| 記号 | 採用品／定数 | JLC/LCSC番号 | 1枚分 | 2枚分 |
|---|---|---|---:|---:|
| C19、C22、C24 | CL10A475KO8NNNC、4.7µF、0603 | C19666 | 3 | 6 |
| C20、C21 | 0402CG150J500NT、15pF、0402 | C1548 | 2 | 4 |
| L1 | AOTA-B201610S3R3-101-T、3.3µH | C42411119 | 1 | 2 |
| Q1 | HJC／hongjiacheng MMBT3906 | C7420354 | 1 | 2 |
| R1、R2 | 0603WAF270JT5E、27Ω、0603 | C25190 | 2 | 4 |
| R3 | 0402WGF330JTCE、33Ω、0402 | C25105 | 1 | 2 |
| R4 | 0402WGF1001TCE、1kΩ、0402 | C11702 | 1 | 2 |
| SW1、SW2 | XUNPU TS-1088-AR02016 | C720477 | 2 | 4 |
| U2 | UTC 78L05G-AB3-R | C71136 | 1 | 2 |
| U3 | Si8621EC-B-IS | C7010821 | 1 | 2 |
| U5 | RP2354A | C41378174 | 1 | 2 |
| U6 | SN65HVD230DR | C12084 | 1 | 2 |
| Y1 | ABM8-272-T3、12MHz | C20625731 | 1 | 2 |

上表は実装数量であり、最小購入数量・実装工程の損耗分を含まない。部品番号は採用済みのものを維持し、SW1/SW2を旧C318884から現在のC720477へ更新した。価格・在庫・Basic/Extended料金の再見積もりはこのファイル更新には含まない。

手実装の扱いは以下のとおり。これらはBOMとCPLの両方から除外している。

- U7：CH340E、[秋月113543](https://akizukidenshi.com/catalog/g/g113543/)、1個／枚・2個／2枚。B面へ手はんだ。
- U4：HTC MAX485ED、秋月購入・手実装。
- U1：RT9080-33GJ5、手持ち・手実装。
- D3/D7/D8：手持ち黄色1608 LED。D1/D10：SS2040FL。D2：PANJIT 1N4148W、秋月購入。
- J1/J16：手持ちUSB-C。J7/J8/J11/J12/SW_0/SW_1/SW_2：XH。J9：XT30PW-M。
- SW3：KHS22E、SW4：手持ちCAN終端スイッチ、SW6：IS-2235-G、いずれも手実装。
- 上表以外の抵抗・コンデンサ：手持ち・手実装。JP1：部品購入ではなく、使用電圧に応じたはんだジャンパ設定。

生成にはインストール済み[Fabrication Toolkit](https://github.com/bennymeg/Fabrication-Toolkit)のProcessManagerを使用した。生成時のみメモリ上で実装対象、LCSC Part #、BOM表示名を指定し、原本の回路図・PCB・プラグインは変更していない。BOOT/RESETのBOM表示を共通型番に揃えたため、同一品番1行に集約されている。

CPLはmm単位、基板の補助原点(0,0)を使用し、X右向き・Y上向き。現PCBは左上が(0,0)なので基板上のY座標は負になる。これは符号の誤りではない。同じ原点で出力した単板Gerberと組み合わせる。各部品の座標はSMDフットプリントのアンカーを用い、任意の平行移動やパネル複製は加えていない。

Toolkitの既知の回転角補正を有効にした。Q1とU2は+180°、U3とU6は+270°、U5は+90°。その他は補正0°。結果を0～360°未満へ正規化したため、KiCadの表示角度とCPLの数値が異なる部品がある。詳細とPCB上のpin1座標はgeneration_manifest.jsonに記録した。

独自フットプリントL1/Y1/SW1/SW2には未知の補正を推測して追加していない。発注画面の部品配置プレビューでは、特にU2/U3/U5/U6/Q1と、L1の向きマークを実PCBのpin1位置に合わせる。L1のpin1は+1.1V側で、PCBを表面から見て上側の端子。JLCの注文固有の配置プレビューは未確認。生成したCPLの回転をそのまま実装保証と扱わない。

検証済み：BOMの13行・18リファレンスとCPLの18行が完全一致、全品番指定あり、全点top、重複・対象漏れ・手実装品の混入なし。全18点の座標と角度をPCBとToolkit補正に対して照合。原本6ファイルのSHA-256が生成前後で一致。

再生成スクリプトは `C:/Users/yasum/Documents/Codex/2026-10-12/sts3215-uart-2-a-iso7731-sn74lvc2g241/work/build_pcba_20261023.py`。KiCad 9付属Pythonで実行すると同チャットのoutputs/PCBA_20261023に再出力する。原本の部品属性は更新していないため、GUIで無設定のままToolkitを実行すると同じPCBA対象にはならない。PCBを変更した場合はこのスクリプトで再生成し、確認後にプロジェクト側のBOM/CPLを更新する。

参照：[JLCPCB BOM要件](https://jlcpcb.com/help/article/bill-of-materials-for-pcb-assembly)、[Fabrication Toolkitの座標・回転補正](https://github.com/bennymeg/Fabrication-Toolkit)、[Q1のJLC掲載メーカーと品番](https://jlcpcb.com/partdetail/hongjiacheng-MMBT3906/C7420354)。Q1はJLC現行画面でhongjiacheng、C7420354、MMBT3906を確認。LCSC側では同じ番号のメーカー表示がR+Oとなっているが、今回の調達先は従来どおりJLCPCB。
