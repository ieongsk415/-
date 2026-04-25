<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>食材收集小遊戲｜意粉關卡</title>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}
body{
  background: #fff8f0;
  padding: 20px;
  text-align: center;
}
/* 目標菜式 */
.dish-emoji{
  font-size: 70px;
  margin-bottom: 8px;
}
.tip-text{
  font-size: 15px;
  color: #666;
  margin-bottom: 25px;
}
/* 購物籃區域 */
.bag{
  width: 160px;
  height: 180px;
  margin: 0 auto 30px;
  background: #e7c9a7;
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 80px;
}
/* 食材Emoji格 */
.material-wrap{
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  justify-content: center;
  margin-bottom: 35px;
}
.item{
  width: 90px;
  height: 90px;
  background: #ffffff;
  border: 2px solid #ddd;
  border-radius: 12px;
  font-size: 45px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: grab;
  user-select: none;
}
.item:active{
  cursor: grabbing;
}
/* 下方6個收集格 */
.box-row{
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 30px;
}
.box{
  width: 55px;
  height: 55px;
  border: 2px dashed #cc9966;
  border-radius: 10px;
  background: #fff;
}
/* 下一關按鈕 */
.next-btn{
  padding: 12px 35px;
  background: #22aa66;
  color: #fff;
  border: none;
  border-radius: 10px;
  font-size: 17px;
  display: none;
  cursor: pointer;
}
</style>
</head>
<body>

<!-- 目標菜式：意粉 Emoji -->
<div class="dish-emoji">🍝</div>
<div class="tip-text">提示：只可放入意粉需要嘅食材</div>

<!-- 換咗：購物籃 🛒 -->
<div class="bag" id="bag">🛒</div>

<!-- 食材：全部 iPhone Emoji -->
<div class="material-wrap">
  <!-- 正確食材 6樣 -->
  <div class="item" draggable="true" data-correct="yes">🍝</div>
  <div class="item" draggable="true" data-correct="yes">🍅</div>
  <div class="item" draggable="true" data-correct="yes">🧅</div>
  <div class="item" draggable="true" data-correct="yes">🧀</div>
  <div class="item" draggable="true" data-correct="yes">🥩</div>
  <div class="item" draggable="true" data-correct="yes">🫒</div>

  <!-- 錯誤食材 亂入 -->
  <div class="item" draggable="true" data-correct="no">🐟</div>
  <div class="item" draggable="true" data-correct="no">🥬</div>
  <div class="item" draggable="true" data-correct="no">🍖</div>
</div>

<!-- 六格收集位 -->
<div class="box-row">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>

<button class="next-btn" id="nextBtn">前往下一關</button>

<script>
const items = document.querySelectorAll('.item');
const bag = document.getElementById('bag');
const boxes = document.querySelectorAll('.box');
const nextBtn = document.getElementById('nextBtn');

let count = 0;

// 拖拉功能
items.forEach(item => {
  item.addEventListener('dragstart', e => {
    e.dataTransfer.setData('text', item.dataset.correct);
  });
});

bag.addEventListener('dragover', e => e.preventDefault());
bag.addEventListener('drop', e => {
  e.preventDefault();
  let result = e.dataTransfer.getData('text');

  // 揀啱先入格
  if(result === "yes" && count < 6){
    boxes[count].style.background = "#ffe8cc";
    count++;
    // 可選：將食材emoji都顯示入格入面
    boxes[count-1].innerText = e.target.innerText;
    boxes[count-1].style.fontSize = "30px";
    boxes[count-1].display = "flex";
    boxes[count-1].alignItems = "center";
    boxes[count-1].justifyContent = "center";
  }

  // 6格滿 解鎖按鈕
  if(count >= 6){
    nextBtn.style.display = "inline-block";
  }
});

nextBtn.onclick = function(){
  alert("✅ 食材收集完成！可以進入下一關");
}
</script>

</body>
</html>
