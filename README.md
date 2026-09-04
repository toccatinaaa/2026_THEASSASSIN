#### ゲーム概要

    TPS&FPSの3Dシューティングゲーム。
    弓使いのアサシンになり、同業のターゲットを始末する任務をこなします。

#### 操作方法

    ・WASDで移動
    ・右クリックホールドでFPSの照準モードに切り替え＆弓をチャージ
    ・チャージされた状態で左クリックすると射撃
    ・Qキーホールドでターゲットの位置をUIで表示
    ・ESC / M キーでMenuを開く
    ・ALTキーホールドでカーソル表示

#### 実装した機能
###### A. 3Dカメラの概念と演出（プレイヤー追従カメラなど）

    FPSカメラとTPSカメラのスムーズな切り替えを行いました。
    TPSではCinemachineのThirdPersonFollow、FPSではHard Lock To Targetと
    InputAxisControllerを使用しています。
    カメラを切り替える際に違和感がないように、TPSとFPSのカメラの角度を同期させるなど工夫しました。
    マウス操作でカメラを移動するとカーソルが画面の外に出た際バグってしまうので、
    カーソルをロック、非表示にしました。

###### B. URPを用いた高品質な3Dシーン構築（ポストエフェクト、ライトの設定など）

    ライトはDirectional Lightを使い木漏れ日ができるように、ポストエフェクトは
    Shadows Midtones HighlightsとColor Curvesで色を寒色に調整、
    Depth Of Fieldを使用してゲームシーンでは遠くをぼかし、StartMenuでは完全に背景をぼかしました。
    また、StartMenuはVignetteも使い周囲を暗くすることで中心に視線が集中するようにしています。

###### E. 3Dモデルのアニメーション制御（Blend Treeによる移動遷移、Animatorレイヤーの分離、またはIKによるGrounding/LookAtなど）
    
    StateMachineデザインパターンを使い、Animationを細かく分けました。
    Animationの遷移はBoolで分けており、各ステートに入った際boolをtrueに、出た時falseにして制御しています。
    弓は引きはじめ、引いてホールドするIdle、撃った時の三つで分かれています。
    落下するとFallingになり、着地するとLandingからIdleに遷移します。
