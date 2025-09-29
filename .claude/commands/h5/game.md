---
description: 创建H5游戏项目
argument-hint: [游戏名称]
allowed-tools: Write(*), Edit(*), Bash(*)
---

# 🎮 H5游戏开发

开发 $ARGUMENTS H5游戏：

## 1. 游戏引擎选择
```javascript
// Phaser 3游戏引擎
import Phaser from 'phaser';

class GameScene extends Phaser.Scene {
  constructor() {
    super({ key: '${ARGUMENTS}Scene' });
  }

  preload() {
    // 加载游戏资源
    this.load.image('player', 'assets/player.png');
    this.load.image('enemy', 'assets/enemy.png');
    this.load.audio('bgm', 'assets/background.mp3');
  }

  create() {
    // 创建游戏对象
    this.player = this.add.sprite(400, 300, 'player');
    this.enemies = this.add.group();

    // 设置物理效果
    this.physics.add.collider(this.player, this.enemies, this.hitEnemy, null, this);

    // 输入控制
    this.cursors = this.input.keyboard.createCursorKeys();
  }

  update() {
    // 游戏循环更新
    this.handleInput();
    this.updateEnemies();
  }

  handleInput() {
    if (this.cursors.left.isDown) {
      this.player.x -= 5;
    }
    if (this.cursors.right.isDown) {
      this.player.x += 5;
    }
  }
}

// 游戏配置
const config = {
  type: Phaser.AUTO,
  width: 800,
  height: 600,
  physics: {
    default: 'arcade',
    arcade: {
      gravity: { y: 300 },
      debug: false
    }
  },
  scene: GameScene
};

const game = new Phaser.Game(config);
```

## 2. 移动端适配
```javascript
// 响应式游戏布局
class ResponsiveGame {
  constructor() {
    this.setupResize();
    this.setupTouch();
  }

  setupResize() {
    window.addEventListener('resize', () => {
      this.resizeGame();
    });
  }

  setupTouch() {
    // 虚拟手柄
    this.virtualGamepad = new VirtualGamepad();
  }

  resizeGame() {
    const canvas = document.querySelector('canvas');
    const windowWidth = window.innerWidth;
    const windowHeight = window.innerHeight;

    // 计算缩放比例
    const scale = Math.min(windowWidth / 800, windowHeight / 600);
    canvas.style.transform = `scale(${scale})`;
  }
}
```

## 3. 性能优化
- 对象池管理
- 纹理图集优化
- 音频压缩
- 帧率控制

## 4. 发布配置
```javascript
// 构建优化
const gameConfig = {
  // 生产环境配置
  physics: {
    default: 'arcade',
    arcade: {
      debug: false // 关闭调试模式
    }
  },
  // 资源预加载
  preloader: {
    showProgressBar: true,
    progressBarColor: '#ff6b6b'
  }
};
```

游戏名称：$ARGUMENTS