<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>時間軸動畫</title>
  <style>
    /* 基本樣式 */
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      height: 400vh; /* 確保有足夠滾動空間 */
      background-color: #f0f0f0;
    }

    /* 時間軸容器 */
    .timeline {
      position: relative;
      width: 50%;
      margin: 0 auto;
      padding-top: 50px;
      height: 300vh; /* 設定時間軸高度至少為 300vh */
    }

    /* 時間軸的直線 */
    .line {
      position: absolute;
      left: 50%;
      top: 0;
      width: 4px;
      height: 300vh; /* 直線高度為 300vh */
      background-color: #007bff;
      transform: translateX(-50%);
    }

    /* 時間軸上的項目 */
    .timeline-item {
      position: relative;
      margin: 50px 0;
      padding: 20px;
      width: 60%;
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      opacity: 0; /* 初始為不可見 */
      transform: translateY(-100px); /* 初始向上移動 -100px（畫面上方） */
      transition: opacity 1.5s ease-out, transform 1.5s ease-out; /* 延長浮現時間 */
    }

    /* 動畫進入效果 */
    .timeline-item.visible {
      opacity: 1;
      transform: translateY(0); /* 平滑移入 */
    }

    /* 左右交替顯示 */
    .timeline-item:nth-child(odd) {
      left: 55%;
      transform: translateX(-50%) translateY(-100px);
    }

    .timeline-item:nth-child(even) {
      left: 45%;
      transform: translateX(-50%) translateY(-100px);
    }
  </style>
</head>
<body>
  <div class="timeline">
    <div class="line"></div>
    <!-- 10 個時間軸項目 -->
    <div class="timeline-item">歷史事件 1 - 發生了某個重要事件</div>
    <div class="timeline-item">歷史事件 2 - 另一個有趣的事件</div>
    <div class="timeline-item">歷史事件 3 - 重大發現</div>
    <div class="timeline-item">歷史事件 4 - 突破性發展</div>
    <div class="timeline-item">歷史事件 5 - 重要的改變</div>
    <div class="timeline-item">歷史事件 6 - 歷史上的重要人物</div>
    <div class="timeline-item">歷史事件 7 - 技術的進步</div>
    <div class="timeline-item">歷史事件 8 - 社會變革</div>
    <div class="timeline-item">歷史事件 9 - 科技創新</div>
    <div class="timeline-item">歷史事件 10 - 現代的重要發展</div>
  </div>

  <script>
    // 取得所有時間軸項目
    const timelineItems = document.querySelectorAll('.timeline-item');

    // 設定 Intersection Observer 參數
    const observerOptions = {
      threshold: 0.1 // 當可見度達到 10% 時觸發
    };

    // 建立 Intersection Observer
    const observer = new IntersectionObserver((entries, observer) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible'); // 當進入畫面時，添加 visible 類別觸發動畫
          observer.unobserve(entry.target); // 停止觀察該元素（避免重複觸發）
        }
      });
    }, observerOptions);

    // 觀察每個時間軸項目
    timelineItems.forEach(item => {
      observer.observe(item);
    });
  </script>
</body>
</html>
