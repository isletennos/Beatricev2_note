# Keywords
YIN法
瞬時周波数(instfreq)
相関特徴量(Autocorrelation Function, ACF)

# modelの入力

# modelの出力

# Beatrice におけるPitchEstimator
下記自分用メモ
・前処理
パディング&フレーム化
rFFT→281bins
下限の64bins (0Hz〜1800Hz)を抽出
・瞬時周波数
spec[1:] * spec[:-1].conj() で隣接フレーム間の位相差を計算
具体例：
spec.shape = [1, 2, 4] # batch=1, bins=2, frames=4 
spec[0, 0, :] = [1+0j, 0.8+0.6j, 0.6+0.8j, 0+1j] # 周波数bin 0 
spec[0, 1, :] = [0+1j, -0.7+0.7j, -1+0j, -0.7-0.7j] # 周波数bin 1

フレーム間 0→1 (bin0): (0.8+0.6j) × (1-0j) = 0.8×1 + 0.6j×1 = 0.8 + 0.6j
フレーム間 1→2 (bin0): (0.6+0.8j) × (0.8-0.6j) = 0.6×0.8 + 0.8×0.8j - 0.6×0.6j + 0.8×0.6 = 0.48 + 0.64j - 0.36j + 0.48 = 0.96 + 0.28j

# YIN法との違い