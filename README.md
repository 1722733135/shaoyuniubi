<html lang="zh-CN">
 <head> 
  <meta charset="UTF-8"> 
  <meta name="viewport" content="width=device-width, initial-scale=1.0"> 
  <title>中考自助查分</title> 
  <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        /* 弹窗样式 */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 999;
            opacity: 1;
            transition: opacity 0.5s ease;
        }
        
        .modal {
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
            text-align: center;
            width: 90%;
            max-width: 500px;
            transform: scale(1);
            transition: transform 0.4s ease;
        }
        
        .modal-header {
            margin-bottom: 20px;
        }
        
        .modal-header h2 {
            color: #2c3e50;
            font-size: 32px;
            margin-bottom: 10px;
            background: linear-gradient(to right, #ff4e50, #f9d423);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .modal-content p {
            color: #7f8c8d;
            font-size: 18px;
            line-height: 1.6;
            margin-bottom: 25px;
        }
        
        .modal-btn {
            background: linear-gradient(to right, #3498db, #8e44ad);
            color: white;
            border: none;
            padding: 14px 35px;
            font-size: 18px;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .modal-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
            background: linear-gradient(to right, #2980b9, #9b59b6);
        }
        
        .modal-btn:active {
            transform: translateY(0);
        }
        
        /* 主体内容样式（默认隐藏） */
        .main-content {
            display: none;
            opacity: 0;
            animation: fadeIn 1s 0.5s forwards;
            flex-direction: column;
            align-items: center;
            position: relative;
        }
        
        .title {
            color: white;
            font-size: 48px;
            margin-bottom: 30px;
            text-align: center;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
        }
        
        .image-container {
            width: 90%;
            max-width: 600px;
            height: 60vh;
            background: linear-gradient(45deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0.2));
            backdrop-filter: blur(20px);
            border-radius: 25px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.4);
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 15px;
        }
        
        .main-image {
            max-width: 100%;
            max-height: 100%;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
            transition: transform 0.5s ease;
        }
        
        .main-image:hover {
            transform: scale(1.03);
        }
        
        .description {
            color: white;
            margin-top: 30px;
            max-width: 600px;
            text-align: center;
            font-size: 18px;
            line-height: 1.6;
            text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        /* 动画关闭状态 */
        .modal-overlay.hide {
            opacity: 0;
            pointer-events: none;
        }
        
        .modal-overlay.hide .modal {
            transform: scale(0.8);
        }
        
        .main-content.show {
            display: flex;
        }
        
        /* 音乐控制样式 */
        .music-control {
            position: absolute;
            bottom: 20px;
            right: 20px;
            z-index: 10;
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(10px);
            padding: 10px 15px;
            border-radius: 30px;
            color: white;
            font-weight: 600;
        }
        
        .music-icon {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            border-radius: 50%;
            transition: background 0.3s;
        }
        
        .music-icon:hover {
            background: rgba(255, 255, 255, 0.2);
        }
        
        .volume-control {
            width: 100px;
            height: 5px;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 3px;
            cursor: pointer;
            position: relative;
        }
        
        .volume-level {
            position: absolute;
            height: 100%;
            width: 70%;
            background: white;
            border-radius: 3px;
            transition: width 0.2s;
        }
        
        .wave-icon {
            display: flex;
            gap: 3px;
            align-items: flex-end;
            height: 25px;
            margin-left: 5px;
        }
        
        .wave {
            width: 4px;
            background: white;
            border-radius: 2px;
        }
        
        .wave:nth-child(1) {
            height: 8px;
        }
        .wave:nth-child(2) {
            height: 12px;
            animation: waveAnimation 1.2s infinite;
            animation-delay: 0.1s;
        }
        .wave:nth-child(3) {
            height: 16px;
            animation: waveAnimation 1.2s infinite;
            animation-delay: 0.2s;
        }
        .wave:nth-child(4) {
            height: 12px;
            animation: waveAnimation 1.2s infinite;
            animation-delay: 0.3s;
        }
        .wave:nth-child(5) {
            height: 8px;
        }
        
        @keyframes waveAnimation {
            0%, 100% { height: 8px; }
            50% { height: 18px; }
        }
        
        .hidden {
            display: none;
        }
    </style> 
  <script src="js/jq.js"></script> 
 </head> 
 <body id="v1"> 
  <!-- 弹窗部分 --> 
  <div class="modal-overlay" id="modal"> 
   <div id="v2" class="modal"> 
    <div id="v3" class="modal-header"> 
     <h2 id="v4">免责声明</h2> 
    </div> 
    <div id="v5" class="modal-content"> 
     <p id="v6">请在人少的地方打开网页</p> 
     <p id="v7">点击下方按钮继续</p> 
     <button class="modal-btn" id="confirmBtn">确认进入</button> 
    </div> 
   </div> 
  </div> 
  <!-- 主体内容 --> 
  <div class="main-content" id="mainContent"> 
   <h1 id="v8" class="title">少羽牛逼
   我为羽家守国门 封杀归来必是神.
   </h1> 
   <div id="v9" class="image-container"> 
    <img id="v18" src="少羽牛逼。.png" alt="自然美景" class="main-image"> 
   </div> 
   <p id="v10" class="description">少羽巅峰时期 2018年少羽杀穿整个自闭城 2019身法创始人 2020年双排9000淘汰分封顶 2021年uzi跳枪一人杀穿职业赛， 2022年追猎干K 2023年六秒灭一休车队 2024年联手职业刺头有了logo 并担任追猎天花板、超体天花板、对掏天花板、歼灭天花板、筷子代言人羽家 随便拿出一个事迹都够一个主播封神了，开挂？他不开照样牛逼，少字开头，羽字结尾 一个他 ，撑起来我的整个青春，你若折他一跟翅膀，我必毁你整个天堂，风雨难改我初心</p> 
   <!-- 音乐控制区 --> 
   <div class="music-control" id="musicControl"> 
    <div class="music-icon" id="playPauseBtn"> 
     <i id="v11" class="fas fa-play"></i> 
    </div> 
    <div class="volume-control" id="volumeControl"> 
     <div class="volume-level" id="volumeLevel"></div> 
    </div> 
    <div class="wave-icon" id="waveIcon"> 
     <div id="v12" class="wave"></div> 
     <div id="v13" class="wave"></div> 
     <div id="v14" class="wave"></div> 
     <div id="v15" class="wave"></div> 
     <div id="v16" class="wave"></div> 
    </div> 
   </div> 
  </div> 
  <!-- 添加音频元素 --> 
  <audio id="bgMusic" loop=""> 
   <source id="v17" src="52.mp3" type="audio/mp3"> 
  </audio> 
  <script>
        document.addEventListener('DOMContentLoaded', function() {
            const modal = document.getElementById('modal');
            const confirmBtn = document.getElementById('confirmBtn');
            const mainContent = document.getElementById('mainContent');
            const bgMusic = document.getElementById('bgMusic');
            const playPauseBtn = document.getElementById('playPauseBtn');
            const volumeControl = document.getElementById('volumeControl');
            const volumeLevel = document.getElementById('volumeLevel');
            const waveIcon = document.getElementById('waveIcon');
            
            // 当前播放状态
            let isPlaying = false;
            
            // 当点击确认按钮时
            confirmBtn.addEventListener('click', function() {
                // 添加hide类触发动画
                modal.classList.add('hide');
                
                // 动画结束后显示主要内容
                setTimeout(function() {
                    mainContent.classList.add('show');
                    
                    // 在用户交互后播放音乐
                    bgMusic.volume = 0.7;
                    bgMusic.play();
                    isPlaying = true;
                    updatePlayIcon();
                }, 500);
            });
            
            // 如果用户点击弹窗外区域也可以关闭弹窗
            modal.addEventListener('click', function(e) {
                if (e.target === modal) {
                    modal.classList.add('hide');
                    setTimeout(function() {
                        mainContent.classList.add('show');
                        bgMusic.play();
                        isPlaying = true;
                        updatePlayIcon();
                    }, 500);
                }
            });
            
            // 播放/暂停按钮点击事件
            playPauseBtn.addEventListener('click', function() {
                togglePlayback();
            });
            
            // 音量控制
            volumeControl.addEventListener('click', function(e) {
                // 计算点击位置相对于音量控制条的位置
                const rect = volumeControl.getBoundingClientRect();
                const pos = (e.clientX - rect.left) / rect.width;
                // 设置音量
                bgMusic.volume = pos;
                volumeLevel.style.width = `${pos * 100}%`;
            });
            
            // 切换播放状态
            function togglePlayback() {
                if (isPlaying) {
                    bgMusic.pause();
                    isPlaying = false;
                } else {
                    bgMusic.play();
                    isPlaying = true;
                }
                updatePlayIcon();
            }
            
            // 更新播放/暂停图标
            function updatePlayIcon() {
                const icon = playPauseBtn.querySelector('i');
                if (isPlaying) {
                    icon.classList.remove('fa-play');
                    icon.classList.add('fa-pause');
                    waveIcon.style.display = 'flex';
                } else {
                    icon.classList.remove('fa-pause');
                    icon.classList.add('fa-play');
                    waveIcon.style.display = 'none';
                }
            }
        });
    </script>  
 </body>
</html>
