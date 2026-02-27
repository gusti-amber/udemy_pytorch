# CIFAR-10 CNN Image Classifier - 画像判定AIアプリ
### サービスURL: https://image-classifier-1osr.onrender.com

PyTorchを用いて開発した画像判定AIアプリです。
公開データセットであるCIFAR-10を使用し、CNN（畳み込みニューラルネットワーク）で学習したモデルをWebアプリケーションに組み込みました。
ユーザーが画像を選択すると、10種類のクラス（乗り物・動物）の中から最も確率の高いクラスを予測します。

## CIFAR-10とは

CIFAR-10は、カナダのトロント大学によって公開された画像分類用データセットです。
32×32ピクセルのカラー画像60,000枚（学習用50,000枚・テスト用10,000枚）で構成され、以下の10クラスに分類されています。

* airplane
* automobile
* bird
* cat
* deer
* dog
* frog
* horse
* ship
* truck

画像分類の入門用データセットとして広く利用されています。

## 技術スタック

| カテゴリ         | 技術                              |
| ------------ | ------------------------------- |
| スタイリング           | Tailwind CSS / daisyUI          |
| バックエンド           | Python 3.12.12                  |
| 機械学習フレームワーク  | PyTorch (torch 2.5.1)           |
| データセット / 前処理 | torchvision 0.20.1, numpy 2.4.2 |
| 画像処理         | Pillow 12.1.0                   |
| Webフレームワーク   | Flask 3.1.2                     |
| テンプレートエンジン   | Jinja2 3.1.6                    |
| WSGI / サーバー  | Werkzeug 3.1.3, gunicorn 25.0.1 |
| インフラ       | Render                          |

## 本アプリのポイント

### CIFAR-10を使用したCNNによる訓練モデルの実装
* **GPU環境での訓練 → CPU環境での本番運用を実現**

  Google Colab（GPU）で学習したモデルを保存し、CPU環境のWebアプリケーション上で推論できる構成を実装しました。`map_location` を用いて実行環境の違いを吸収しています。

* **モデルの保存・読み込みの理解と実装**

  `state_dict()` によるパラメータ管理、`torch.save()` / `load_state_dict()` を用いた永続化処理を実装し、学習と推論を分離した設計にしています。

* **データ拡張による汎化性能の向上**

   `RandomAffine` や `RandomHorizontalFlip` を用いたデータ拡張を取り入れ、過学習の抑制とモデルの汎化性能向上を図りました。

<img width="2649" height="1366" alt="image" src="https://github.com/user-attachments/assets/7d4ffa44-6543-44dd-b5b5-c4f738f4954a" />



* **学習過程の可視化と検証**

  訓練誤差・テスト誤差を記録し、エポックごとの推移を可視化することで、学習状況を定量的に分析できるようにしました。

<img width="2649" height="728" alt="image" src="https://github.com/user-attachments/assets/58ceae0e-1f31-4f56-b77d-d133a6fd4da1" />



* **学習モードと評価モードの適切な切り替え**

  `train()` / `eval()` を適切に切り替え、Dropoutの挙動を考慮した正しい学習・推論フローを実装しています。


## 参考資料

### CIFAR-10 公式サイト

https://www.cs.toronto.edu/~kriz/cifar.html

### PyTorchによるCNN実装を学んだ講座

https://www.udemy.com/course/ai-pytorch/
