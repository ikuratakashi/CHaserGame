Pythonで生成した音声をそのまま再生するには、`pydub`ライブラリを使うと便利です。以下に、先ほどのFM音源生成コードに音声再生機能を追加した例を示します。

### 必要なライブラリのインストール
まず、`pydub`と`simpleaudio`をインストールします。

```sh
pip install pydub simpleaudio
```

### 音声再生を追加したコード

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.io.wavfile import write
from pydub import AudioSegment
from pydub.playback import play

# サンプリングレートと時間軸の設定
sampling_rate = 44100
duration = 1.5  # 秒
t = np.linspace(0, duration, int(sampling_rate * duration), endpoint=False)

# 音階の周波数
notes = {
    'E4': 329.63,
    'G#4': 415.30,
    'B4': 493.88,
    'E5': 659.25,
    'G#5': 830.61,
    'B5': 987.77
}

# 各音の持続時間
note_durations = [0.3, 0.3, 0.3, 0.3, 0.3, 0.3]

# FM音源の生成
audio = np.zeros_like(t)
start = 0

for note, duration in zip(notes.values(), note_durations):
    end = start + int(sampling_rate * duration)
    modulator = np.sin(2.0 * np.pi * note * t[start:end]) * 2.0
    carrier = np.sin(2.0 * np.pi * note * t[start:end] + modulator)
    audio[start:end] += carrier * 0.5
    start = end

# 音声データの正規化
audio = audio * (32767 / np.max(np.abs(audio)))
audio = audio.astype(np.int16)

# WAVファイルとして保存
wav_file = "windows95_startup_fm.wav"
write(wav_file, sampling_rate, audio)

# 音声の再生
sound = AudioSegment.from_wav(wav_file)
play(sound)

# 波形のプロット
plt.plot(t[:1000], audio[:1000])
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.title("FM Synthesis Waveform")
plt.show()
```

### 説明
- **pydubとsimpleaudioのインストール**: `pydub`は音声ファイルの操作に便利なライブラリで、`simpleaudio`は音声再生をサポートします。
- **音声の再生**: `pydub`の`AudioSegment`を使ってWAVファイルを読み込み、`play`関数で再生します。

このコードを実行すると、生成されたFM音源の音声が再生されます。試してみて、どのように感じたか教えてくださいね！他にも質問があればどうぞ。
