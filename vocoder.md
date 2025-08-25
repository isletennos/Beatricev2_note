# Keywords
DDSP

# modelの入力
(後で日本語+図に直す)
x = (
            self.embed_phone(phone)
            + self.embed_quantized_pitch(quantized_pitch).transpose(1, 2)
            + self.embed_pitch_features(pitch_features)
            + (
                self.embed_speaker(target_speaker_id)[:, :, None]
                + self.embed_formant_shift(formant_shift_indices)[:, :, None]
            )
        )
# modelの出力
音声 + 
{
            "periodic_signal": periodic_signal.detach(),
            "aperiodic_signal": aperiodic_signal.detach(),
            "noise_excitation": noise_excitation.detach(),
        }

# DDSPとは
ここにDDSPの説明

# Beatrice におけるDDSP(PseudoDDSPVocoder)
入力特徴量からIRから予測。この時のモデルはConvNeXt Block
ピッチ情報とIRから周期信号(Harmonic Synthesis)を生成

入力特徴量から非周期性パラメータを予測。この時のモデルもConvNeXt Block
非周期性パラメータからノイズ信号(Filtered Noise)を生成

周期信号(Harmonic Synthesis)とノイズ信号(Filtered Noise)を加算して最終的な音声信号を出力

## アーティファクト防止

# DDSP-SVCとの比較
