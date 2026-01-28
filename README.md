# Chaoxing-Homework
//用于超星学习通作业批改赋分的油猴脚本
// ==UserScript==
// @name         学习通教师自动批阅
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  学习通批改作业点击ctrl直接触发"提交并进入下一份"
// @match        *://*.chaoxing.com/*
// @icon         data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==
// @grant        none
// @license      End-User License Agreement
// ==/UserScript==

(function() {
    'use strict';

    document.onkeyup = function(e) {
        var event = e || window.event;
        var key = event.which || event.keyCode || event.charCode;

        // 监听 Ctrl 键 (Key Code 17)
        if (key == 17) {
            // 随机赋分
            var scores = [60, 70, 80, 90];
            var randomScore = scores[Math.floor(Math.random() * scores.length)];

            var scoreInput = document.getElementById('tmpscore');
            if (scoreInput) {
                scoreInput.value = randomScore;
                scoreInput.dispatchEvent(new Event('change', { bubbles: true }));
                console.log("已自动填入成绩：" + randomScore + "分");
            }

           var targetBtn = document.querySelector('a[onclick="markAction(0)"]');

              if (targetBtn) {
                  targetBtn.click();
                  console.log("检测到Ctrl键，已自动点击提交下一份");

                  // 延迟点击 checkpass 按钮，确保前一个操作完成
                  setTimeout(function() {
                      var checkPassBtn = document.querySelector('a[onclick="checkPass()"]');
                      if (checkPassBtn) {
                          checkPassBtn.click();
                          console.log("已自动点击 checkpass 按钮");
                      } else {
                          console.log("未找到 checkpass 按钮");
                      }
                  }, 500); // 500毫秒延迟，可根据需要调整

              } else {
                  console.log("未找到提交按钮");
              }
        }
    };
})();
