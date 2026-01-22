document.addEventListener("DOMContentLoaded", () => {
    // --- 1. 漢堡選單功能 ---
    const hamburger = document.getElementById("hamburger");
    const navLinks = document.getElementById("nav-links");

    if (hamburger) {
        hamburger.addEventListener("click", () => {
            navLinks.classList.toggle("active");
        });
    }

    // 點擊連結後自動關閉選單 (手機版優化)
    document.querySelectorAll(".nav-links a").forEach(link => {
        link.addEventListener("click", () => {
            navLinks.classList.remove("active");
        });
    });

    // --- 2. 打字動畫邏輯 ---
    const introText = "禪門廣現清淨法，悅心悅已悅眾生。\n潛龍驚動天地心，能現諸法巧應生。\n開天闢地精⾏善，發⼼廣⾏妙善⽤。\n學習成長以應心，苑苑傳承道根本。";
    const typingTarget = document.querySelector("#intro .content-box p");
    let typingTimer = null;

    function startTyping() {
        if (!typingTarget) return;
        typingTarget.innerHTML = ""; // 先清空文字
        let index = 0;
        
        clearInterval(typingTimer);
        typingTimer = setInterval(() => {
            if (index < introText.length) {
                const char = introText.charAt(index);
                typingTarget.innerHTML += char === "\n" ? "<br>" : char;
                index++;
            } else {
                clearInterval(typingTimer);
            }
        }, 70); // 這裡可以調整打字速度 (毫秒)
    }

    // --- 3. 滾動觀察器 (整合所有動畫) ---
    // 每次進入/離開視窗都會觸發
    const observerOptions = {
        threshold: 0.15 // 元素出現 15% 時觸發
    };

    const scrollObserver = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                // 當元素進入視窗：播放動畫
                entry.target.classList.add("reveal-active");

                // 如果是宗旨區塊，額外啟動打字動畫
                if (entry.target.id === "intro") {
                    startTyping();
                }
            } else {
                // 當元素離開視窗：移除標籤，重置狀態以利下次重播
                entry.target.classList.remove("reveal-active");
                
                // 如果是宗旨區塊，離開時清空文字
                if (entry.target.id === "intro" && typingTarget) {
                    typingTarget.innerHTML = "";
                    clearInterval(typingTimer);
                }
            }
        });
    }, observerOptions);

    // 將所有需要動畫的 Section 加入觀察
    document.querySelectorAll("section").forEach(sec => {
        sec.classList.add("reveal-init"); // 初始化動畫狀態
        scrollObserver.observe(sec);
    });
});
