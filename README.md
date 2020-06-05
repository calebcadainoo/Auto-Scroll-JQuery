# Auto-Scroll-JQuery
Automatically scroll list items that overflow their container more like a list view

### HTML
```sh
<div class="dash-am-list">
            <div class="dash-am-scroll trans">
                <?php for ($i=0; $i < 15; $i++) { ?>
                    <!-- grid -->
                    <div id="dash-mem-<?= $i ?>" class="am-member-grid">
                        <div class="am-member-pic imgfx">
                            <img src="./app-data/choir/5ed27d7f792fe-1590852991.jpg" alt="Admin Name">
                        </div>
                        <div class="am-member-fname">Caleb</div>
                    </div>
                <?php } ?>
            </div>
        </div>
```

### CSS
```sh
.dash-am-list{
    width: 100%;
    height: 120px;
    overflow: hidden;
    /* padding: 10px; */
    /* background-color: #fff; */
}

.dash-am-scroll{
    overflow-x: auto;
    padding-bottom: 30px;
    position: relative;
    left: 0;
}

.am-member-grid{
    float: left;
    padding: 10px;
    padding-right: 14px;
    text-align: center;
    box-sizing: content-box;
}

.am-member-pic{
    width: 50px;
    height: 50px;
    margin: auto;
    margin-bottom: 10px;
    border-radius: 50%;
    font-size: 8px;
}

.am-member-fname{
    font-size: 10px;
    font-weight: 300;
    text-transform: uppercase;
    color: rgba(0, 0, 0, 0.7);
}
```

### JS
```sh
let dashMembersNum = $('.am-member-grid').length;
    let dashGridWidth = $('.am-member-grid').width() + 24; // 24 is the padding 10 + 14
    let scrollView = $('.dash-am-scroll');
    var dashList = $('.dash-am-list');
    // set scroll view width
    scrollView.width((dashGridWidth * dashMembersNum) + 'px');

    var gridsInView = dashList.width() / dashGridWidth;

    var gridsOutView = dashMembersNum - gridsInView;

    var gridsOutViewWhole = Math.floor(gridsOutView);

    var incVal = (gridsOutView - gridsOutViewWhole);

    console.log('Grids In View: ' + gridsInView);
    console.log('Grids Out View: ' + gridsOutView);
    console.log('Grids Out View Whole: ' + gridsOutViewWhole);
    console.log('Inc Val: ' + incVal)

    if (scrollView.width() > dashList.width()) {
        var leftPos = 0;
        let minus = gridsOutViewWhole;
        setInterval(function (){
            leftPos -= dashGridWidth;
            minus -= 1;
            if (minus < -1) {
                leftPos = 0;
                minus = gridsOutViewWhole;
            }
            scrollView.css({
                'left': leftPos + 'px'
            });
            // console.log(leftPos + 'px');
        }, 3000);
    }
```
