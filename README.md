#### ゲーム概要

    TPS&FPSの3Dシューティングゲーム。
    弓使いのアサシンになり、同業のターゲットを始末する任務をこなします。

#### 操作方法

    WASDで移動
    右クリックホールドでFPSの照準モードに切り替え
    右クリックホールドで弓をチャージしたら左クリックで矢を撃つ
    Qキーホールドでターゲットの位置をUIで表示

#### 実装した機能
###### A. 3Dカメラの概念と演出（プレイヤー追従カメラなど）

    FPSカメラとTPSカメラのスムーズな切り替えを行いました。
    TPSではCinemachineのThirdPersonFollow、FPSではHard Lock To Targetと
    InputAxisControllerを使用しています。
    カメラを切り替える際に違和感がないように、TPSとFPSのカメラの角度を同期させるなど工夫しました。

###### B. URPを用いた高品質な3Dシーン構築（ポストエフェクト、ライトの設定など）

    ライトはDirectional Lightを使い木漏れ日ができるように、ポストエフェクトは
    Shadows Midtones HighlightsとColor Curvesで色を寒色に調整、
    Depth Of Fieldを使用してゲームシーンでは遠くをぼかし、StartMenuでは完全に背景をぼかしました。
    また、StartMenuはVignetteも使い周囲を暗くすることで中心に視線が集中するようにしています。

###### E. 3Dモデルのアニメーション制御（Blend Treeによる移動遷移、Animatorレイヤーの分離、またはIKによるGrounding/LookAtなど）
    
    StateMachineデザインパターンを使い、Animationを細かく分けました。
    Animationの遷移はBoolで分けており、各ステートに入った際(Enter)にboolをtrueに、出た時(Exit)にして制御しています。
    弓は引きはじめ、引いてホールドするIdle、撃った時の三つで分かれています。
    
