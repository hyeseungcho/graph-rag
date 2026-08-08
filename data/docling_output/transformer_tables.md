# Transformer 논문 - 테이블 추출 결과

## 테이블 1
- 페이지: 6
- 레벨: 1

| Layer Type                  | Complexity per Layer   | Sequential Operations   | Maximum Path Length   |
|:----------------------------|:-----------------------|:------------------------|:----------------------|
| Self-Attention              | O ( n 2 · d )          | O (1)                   | O (1)                 |
| Recurrent                   | O ( n · d 2 )          | O ( n )                 | O ( n )               |
| Convolutional               | O ( k · n · d 2 )      | O (1)                   | O ( log k ( n ))      |
| Self-Attention (restricted) | O ( r · n · d )        | O (1)                   | O ( n/r )             |

---

## 테이블 2
- 페이지: 8
- 레벨: 1

| Model.                          |   BLEU.EN-DE |   BLEU.EN-FR | Training Cost (FLOPs).EN-DE   | Training Cost (FLOPs).EN-FR   |
|:--------------------------------|-------------:|-------------:|:------------------------------|:------------------------------|
| ByteNet [18]                    |        23.75 |              |                               |                               |
| Deep-Att + PosUnk [39]          |              |        39.2  |                               | 1 . 0 · 10 20                 |
| GNMT + RL [38]                  |        24.6  |        39.92 | 2 . 3 · 10 19                 | 1 . 4 · 10 20                 |
| ConvS2S [9]                     |        25.16 |        40.46 | 9 . 6 · 10 18                 | 1 . 5 · 10 20                 |
| MoE [32]                        |        26.03 |        40.56 | 2 . 0 · 10 19                 | 1 . 2 · 10 20                 |
| Deep-Att + PosUnk Ensemble [39] |              |        40.4  |                               | 8 . 0 · 10 20                 |
| GNMT + RL Ensemble [38]         |        26.3  |        41.16 | 1 . 8 · 10 20                 | 1 . 1 · 10 21                 |
| ConvS2S Ensemble [9]            |        26.36 |        41.29 | 7 . 7 · 10 19                 | 1 . 2 · 10 21                 |
| Transformer (base model)        |        27.3  |        38.1  | 3 . 3 · 10 18                 | 3 . 3 · 10 18                 |
| Transformer (big)               |        28.4  |        41.8  | 2 . 3 · 10 19                 | 2 . 3 · 10 19                 |

---

## 테이블 3
- 페이지: 9
- 레벨: 1

|      | N                                         | d model                                   | d ff                                      | h                                         | d k                                       | d v                                       | P drop                                    | ϵ ls                                      | train steps   |   PPL (dev) |   BLEU (dev) |   params × 10 6 |
|:-----|:------------------------------------------|:------------------------------------------|:------------------------------------------|:------------------------------------------|:------------------------------------------|:------------------------------------------|:------------------------------------------|:------------------------------------------|:--------------|------------:|-------------:|----------------:|
| base | 6                                         | 512                                       | 2048                                      | 8                                         | 64                                        | 64                                        | 0.1                                       | 0.1                                       | 100K          |        4.92 |         25.8 |              65 |
|      |                                           |                                           |                                           | 1                                         | 512                                       | 512                                       |                                           |                                           |               |        5.29 |         24.9 |                 |
|      |                                           |                                           |                                           | 4                                         | 128                                       | 128                                       |                                           |                                           |               |        5    |         25.5 |                 |
| (A)  |                                           |                                           |                                           | 16                                        | 32                                        | 32                                        |                                           |                                           |               |        4.91 |         25.8 |                 |
|      |                                           |                                           |                                           | 32                                        | 16                                        | 16                                        |                                           |                                           |               |        5.01 |         25.4 |                 |
|      |                                           |                                           |                                           |                                           | 16                                        |                                           |                                           |                                           |               |        5.16 |         25.1 |              58 |
| (B)  |                                           |                                           |                                           |                                           | 32                                        |                                           |                                           |                                           |               |        5.01 |         25.4 |              60 |
|      | 2                                         |                                           |                                           |                                           |                                           |                                           |                                           |                                           |               |        6.11 |         23.7 |              36 |
|      | 4                                         |                                           |                                           |                                           |                                           |                                           |                                           |                                           |               |        5.19 |         25.3 |              50 |
|      | 8                                         |                                           |                                           |                                           |                                           |                                           |                                           |                                           |               |        4.88 |         25.5 |              80 |
| (C)  |                                           | 256                                       |                                           |                                           | 32                                        | 32                                        |                                           |                                           |               |        5.75 |         24.5 |              28 |
|      |                                           | 1024                                      |                                           |                                           | 128                                       | 128                                       |                                           |                                           |               |        4.66 |         26   |             168 |
|      |                                           |                                           | 1024                                      |                                           |                                           |                                           |                                           |                                           |               |        5.12 |         25.4 |              53 |
|      |                                           |                                           | 4096                                      |                                           |                                           |                                           |                                           |                                           |               |        4.75 |         26.2 |              90 |
|      |                                           |                                           |                                           |                                           |                                           |                                           | 0.0                                       |                                           |               |        5.77 |         24.6 |                 |
|      |                                           |                                           |                                           |                                           |                                           |                                           | 0.2                                       |                                           |               |        4.95 |         25.5 |                 |
| (D)  |                                           |                                           |                                           |                                           |                                           |                                           |                                           | 0.0                                       |               |        4.67 |         25.3 |                 |
|      |                                           |                                           |                                           |                                           |                                           |                                           |                                           | 0.2                                       |               |        5.47 |         25.7 |                 |
| (E)  | positional embedding instead of sinusoids | positional embedding instead of sinusoids | positional embedding instead of sinusoids | positional embedding instead of sinusoids | positional embedding instead of sinusoids | positional embedding instead of sinusoids | positional embedding instead of sinusoids | positional embedding instead of sinusoids |               |        4.92 |         25.7 |                 |
| big  | 6                                         | 1024                                      | 4096                                      | 16                                        |                                           |                                           | 0.3                                       |                                           | 300K          |        4.33 |         26.4 |             213 |

---

## 테이블 4
- 페이지: 10
- 레벨: 1

| Parser                             | Training                 |   WSJ 23 F1 |
|:-----------------------------------|:-------------------------|------------:|
| Vinyals &Kaiser el al. (2014) [37] | WSJ only, discriminative |        88.3 |
| Petrov et al. (2006) [29]          | WSJ only, discriminative |        90.4 |
| Zhu et al. (2013) [40]             | WSJ only, discriminative |        90.4 |
| Dyer et al. (2016) [8]             | WSJ only, discriminative |        91.7 |
| Transformer (4 layers)             | WSJ only, discriminative |        91.3 |
| Zhu et al. (2013) [40]             | semi-supervised          |        91.3 |
| Huang &Harper (2009) [14]          | semi-supervised          |        91.3 |
| McClosky et al. (2006) [26]        | semi-supervised          |        92.1 |
| Vinyals &Kaiser el al. (2014) [37] | semi-supervised          |        92.1 |
| Transformer (4 layers)             | semi-supervised          |        92.7 |
| Luong et al. (2015) [23]           | multi-task               |        93   |
| Dyer et al. (2016) [8]             | generative               |        93.3 |

---

