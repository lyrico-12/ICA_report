# ICA_report
プログラミング基礎演習の期末レポート
独立主成分分析を実装する。
```c
#　Independent Component Analysis
def ica(seed):
    global mat_z # 観測データを白色化した行列
    mat_z = np.asarray(mat_z)
    np.random.seed(seed)
    w_prev = np.random.rand(2, 1)
    w_prev = w_prev / np.linalg.norm(w_prev)
    w = w_prev
    compare = np.array([[10, 10, 10]])

    while np.linalg.norm(compare) > 1e-9:
        zwz3 = mat_z * ((w_prev.T @ mat_z) ** 3)
        zwz3 = zwz3.mean(axis = 1).reshape(-1, 1)
        w = zwz3 - 3 * w_prev
        if w[0] < 0:
            w = -w
        w = w / np.linalg.norm(w)
        compare = w_prev - w
        w_prev = w
        
    mat_z = np.asmatrix(mat_z)
    return w
```
尖度を用いた独立成分分析の実装を上のような関数で行った。課題1-3は基本的にこの関数によってデータを分離してくる。
- kadai1 異なる２つの混合波形の分離
- kadai2 エリーゼのためにとトルコ行進曲が重なった音源を分離
- kadai2_sub 3人の英語話者の話を分離
- kadai3 二人の女性の顔写真を分離