# AHC013

## adhoc 考察
- TLは3secです

- seedによってSolverの切り替えが必要になりそう
    - Kの大きさ
    - 密度

- 最終の配置を決め打ちすると最適な移動が求まる？
- Connectの方法によっては別のConnectが阻害されることがある

- 配置が決まったときに最も高いスコアになるConnectを求めることができるか
    - x個同じ + y個同じ : + x*y 点 
        - 全体で (x+1) * x / 2 点
    - x個同じ + y個異なる : - x*y点 
        - 全体で (x+1) * x / 2 + (y+1) * y / 2 - x*y 点
    
- できるだけ少ないMoveの後、たくさんConnectしたい
    - Moveだけ焼きなましとかビームで、ConnectはDPとかフローとか貪欲とか(中身は何も考えていない)みたいな感じか？

## メタヒューリスティクス考察
- Move, Connectを一緒にまとめて焼きなまし？
    - Move <-> Move
        - 削除して挿入とか(テキトー)
        - Moveの変更は差分だけ計算みたいなことができない
        - 後ろの方の全部が影響されるのでヤバイ
            - スコア計算し直しどころではなく、後ろの全部の整合性が合わなくなる
    - Connect <-> Connect
    - Move <-> Connect

- Move, Connectを別々にやる焼きなまし
    - 言ってみただけ


- ビームサーチ


## 実装考察
- Score 計算高速化
- Connect 高速化
    - UFとかででやると操作を戻したりしないといけないので困る

- 座標は1つのint型で表せる
    - field[N * N]
    - %とか割り算とかをできるだけ使わないような実装は？
    - なんならField自体をlong long型で表せるな
        - (48 * 48) ^ 5 = 64,925,062,108,545,024
        - しかしこれ嬉しいか？

- Move, Connect Action は1つのlong long型で表せる
    - (48 * 48) ^ 4 = 28,179,280,429,056
    - かと言ってこれが嬉しいかというと？
        - 高速に復元できると良い

## TODO
1. pair<int, int> -> int (?)
    - とりあえずどういう実装方針にするか決めた方が良さそう