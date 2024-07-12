# DL基礎講座2024　最終課題「脳波分類」

## 更新

- 2024.06.18 データセットの詳細についての追記
  - データセットの論文はこちらになります（データセットのリンクからもたどれます）．
    - https://elifesciences.org/articles/82580
  - 配布したデータは論文のセクション"MEG data preprocessing and cleaning"の内容が施されたものになります．
    - よってサンプリングレートは200Hzです
  - セクション"MEG data acquisition"に記載のある通り，チャンネルの座標系は[CTF 275 MEG system](https://mne.tools/1.6/auto_examples/visualization/meg_sensors.html#ctf)のものになっております．
    - チャンネル座標をモデルに組み込みたい際の参考にしてください
    - 配布データのチャンネル数が271しかない理由については，上記2セクションに記載のある通りです

## 環境構築

```bash
$ git clone git@github.com:[Github user name]/dl_lecture_competition_pub
```
3. `git checkout`を利用して自身が参加するコンペティションのブランチに切り替える．
- 以下のコマンドを利用して，参加したいコンペティションのブランチに切り替えてください．
- [Competition name]には`MEG-competition`（脳波分類タスク），`VQA-competition`（VQAタスク），`event-camera-competition`（EventCameraタスク）のいずれかが入ります．
```bash
python main.py

# オンラインで結果の可視化（wandbのアカウントが必要）
python main.py use_wandb=True
```

- `outputs/{実行日時}/`に重み`model_best.pt`と`model_last.pt`，テスト入力に対する予測`submission.npy`が保存されます．`submission.npy`をOmnicampusに提出することで，test top-10 accuracyが確認できます．

  - `model_best.pt`はvalidation top-10 accuracyで評価

- 訓練時に読み込む`config.yaml`ファイルは`train.py`，`run()`の`@hydra.main`デコレータで指定しています．新しいyamlファイルを作った際は書き換えてください．

- ベースラインは非常に単純な手法のため，改善の余地が多くあります（セクション「考えられる工夫の例」を参考）．そのため，**Omnicampusにおいてベースラインのtest accuracy=1.637%を超えた提出のみ，修了要件として認めることとします．**

### 評価のみ実行

- テストデータに対する評価のみあとで実行する場合．出力される`submission.npy`は訓練で最後に出力されるものと同じです．

```bash
$ git add main.py hogehoge.txt hugahuga.txt
```
2. `git commit`
- `-m`オプションによりメモを残すことができます．その時の変更によって何をしたか，この後何をするのかなど記録しておくと便利です．
```bash
$ git commit -m "hogehoge"
``` 
3. `git push`
- branch nameには提出方法の手順3でcheckoutの後ろで指定したブランチ名を入力します．
```bash
$ git push origin [branch name]
```

## 最終課題の提出方法
Omnicampusから予測結果(`.npy`)，工夫点レポート(`.pdf`)，実装したコードのリポジトリのURLを提出していただきます．

### 予測結果の提出
1. Omnicampusの「宿題」一覧から「最終課題（---）」をクリックします（---を取り組むタスクに読み替えてください）．
2. 「拡張子（.npy）のファイルを提出」をクリックし，予測結果`.npy`をアップロードします．採点は即時実行され，「リーダーボードへ」をクリックすると，順位表を確認できます．
<img width="1540" alt="submission" src="https://github.com/ailorg/dl_lecture_competition/assets/11865486/ce9eb6b1-5ecb-4f63-88fc-55c46084bd25">

### 工夫点レポートとGithubリポジトリURLの提出
1. Omnicampusの「レポート課題」一覧から「最終課題レポート」をクリックします．
2. 「レポートのタイトル」にレポートの題名（任意のタイトルで構いません），「参照URL」に今回のタスクの実装を含んだGithubリポジトリのURLを入力して，「提出ファイル」で提出ファイル`.pdf`を選択し，「提出する」をクリックします．
<img width="912" alt="report" src="https://github.com/ailorg/dl_lecture_competition/assets/11865486/f0adbb35-5268-4bf2-9e54-3e728cc7f195">

注意：
- 締め切りまでに**何回提出しても構いません**．最後に提出された内容で評価します．

## 課題内容に関する質問について
- 最終課題の内容に関する質問は以下で受け付けています．
  - slack「08_受講生間の疑問解決_最終課題」チャネル
- 基本的には受講生間で解決するようにしてください．**必ずしも全ての質問に対してTAや運営から回答する訳ではないので注意してください**．
