// pizacoupon-website/js/main.js

let siteTour = null; // 將 tour 實例移至外部，以便事件監聽器可以訪問

/**
 * 功能導覽函式 (由 coupon.js 在資料載入後呼叫)
 */
function startSiteTour() {
    // 1. 檢查導覽是否已在執行中，防止重複點擊
    if (siteTour && siteTour.isActive()) {
        return;
    }

    // 2. 確保頁面上至少有一張優惠券卡片，否則不啟動導覽
    if (!document.querySelector('#row .card')) {
        alert("目前沒有優惠券內容可供導覽，請稍後再試。");
        return;
    }
    
    // 建立一個自訂的關閉按鈕 HTML
    const customCancelIcon = '<button type="button" class="tour-close-btn" aria-label="Close">&times;</button>';

    siteTour = new Shepherd.Tour({
        useModalOverlay: true,
        defaultStepOptions: {
            scrollTo: true,
            cancelIcon: {
                enabled: false // 徹底禁用預設的關閉按鈕和 header
            },
        }
    });

    const header = document.querySelector('header');
    const disableStickyHeader = () => header.classList.add('tour-active');
    const enableStickyHeader = () => header.classList.remove('tour-active');

    siteTour.on('show', disableStickyHeader);
    siteTour.on('complete', enableStickyHeader);
    siteTour.on('cancel', enableStickyHeader);

    siteTour.addStep({
        text: `${customCancelIcon}<strong>歡迎來到 PzahaCoupon！</strong><br><br>這是一個快速的功能導覽，將帶您了解如何輕鬆找到最划算的必勝客優惠。`,
        buttons: [
            {
                action() { return this.next(); },
                text: '開始導覽'
            }
        ]
    });

    siteTour.addStep({
        text: `${customCancelIcon}<strong>關鍵字搜尋</strong><br><br>在這裡輸入您想找的關鍵字，例如「比薩」、「雞翅」或優惠代碼，來快速篩選。`,
        attachTo: { element: '#searchInput', on: 'bottom' },
        buttons: [
            { action() { return this.back(); }, secondary: true, text: '上一步' },
            { action() { return this.next(); }, text: '下一步' }
        ]
    });

    siteTour.addStep({
        text: `${customCancelIcon}<strong>內容篩選</strong><br><br>點擊按鈕來篩選包含或排除特定餐點的優惠券。`,
        attachTo: { element: '#contentTagButtons', on: 'bottom' },
        buttons: [
            { action() { return this.back(); }, secondary: true, text: '上一步' },
            { action() { return this.next(); }, text: '下一步' }
        ]
    });

    siteTour.addStep({
        text: `${customCancelIcon}<strong>收藏優惠</strong><br><br>點擊卡片右上角的書籤圖示，就可以收藏您喜歡的優惠券！`,
        attachTo: { element: '#row .card:first-child .bookmark-btn', on: 'bottom' },
        buttons: [
             { action() { return this.back(); }, secondary: true, text: '上一步' },
             { action() { return this.next(); }, text: '下一步' }
        ]
    });

    siteTour.addStep({
        text: `${customCancelIcon}<strong>查看我的收藏</strong><br><br>點擊這裡，就可以只看您收藏過的優惠券。再點一次即可返回所有列表。<br><br><small>請注意：收藏紀錄只會儲存在您的瀏覽器上，清除Cookie或快取可能會導致紀錄遺失。</small>`,
        attachTo: { element: '#favoritesBtn', on: 'bottom' },
        buttons: [
            { action() { return this.back(); }, secondary: true, text: '上一步' },
            { action() { siteTour.complete(); }, text: '完成導覽' }
        ]
    });

    // 移除了自動儲存 "已完成" 狀態到 localStorage 的邏輯
    // 讓使用者可以隨時點擊 "功能導覽" 按鈕重新開始

    siteTour.start();
}


document.addEventListener('DOMContentLoaded', function() {
    // 為我們自訂的關閉按鈕新增事件監聽器
    document.body.addEventListener('click', function(e) {
        if (e.target.matches('.tour-close-btn') && siteTour && siteTour.isActive()) {
            siteTour.cancel();
        }
    });

    // 為手動觸發導覽的按鈕新增事件監聽器
    const startTourBtn = document.getElementById('startTourBtn');
    if (startTourBtn) {
        startTourBtn.addEventListener('click', startSiteTour);
    }

    // Initialize all Bootstrap tooltips on the page
    const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
    [...tooltipTriggerList].map(tooltipTriggerEl => new bootstrap.Tooltip(tooltipTriggerEl));
});
