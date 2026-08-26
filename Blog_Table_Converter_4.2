// ==UserScript==
// @name        Blog Table ⭐ Converter
// @namespace        http://tampermonkey.net/
// @version        4.2
// @description        編集画面上のtable表の表仕様変換ツール
// @author        Ameba Blog User
// @match        https://blog.ameba.jp/ucs/entry/srventryinsertinput.do*
// @match        https://blog.ameba.jp/ucs/entry/srventryupdateinput.do*
// @icon        https://www.google.com/s2/favicons?sz=64&domain=ameblo.jp
// @grant        none
// @updateURL        https://github.com/personwritep/Blog_Table_Converter/raw/main/Blog_Table_Converter.user.js
// @downloadURL        https://github.com/personwritep/Blog_Table_Converter/raw/main/Blog_Table_Converter.user.js
// ==/UserScript==


let retry=0;
let interval=setInterval(wait_target, 100);
function wait_target(){
    retry++;
    if(retry>10){ // リトライ制限 10回 1sec
        clearInterval(interval); }
    let target=document.getElementById('cke_1_contents'); // 監視 target
    if(target){
        clearInterval(interval);
        main(); }}



function main(){
    let ua=0; // Chromeの場合のフラグ
    let agent=window.navigator.userAgent.toLowerCase();
    if(agent.indexOf('firefox') > -1){ ua=1; } // Firefoxの場合のフラグ

    let task=0; // 起動1・作成2・更新3・終了0
    let trim=0; // 追加0・削除1
    let cell_set=0; // セル幅設定パネルの列選択

    let posit_set; // 中央寄せ・左寄せ
    let table_position;
    let border_collapse;
    let add_padd; // td のpadding値
    let layout_fix; // table-layout設定
    let table_border_width;
    let cell_border_width;
    let border_space;
    let left_full; // 左端背景色の優先
    let color_input=[]; // 4個のカラー設定枠
    let word_break; // 英文禁則


    let target=document.getElementById('cke_1_contents'); // 監視 target
    let monitor=new MutationObserver( catch_key );
    monitor.observe(target, {childList: true, attributes: true}); // ショートカット待受け開始

    catch_key();

    function catch_key(){
        if(document.querySelector('.cke_wysiwyg_frame') !=null){ //「通常表示」から実行開始
            let editor_iframe=document.querySelector('.cke_wysiwyg_frame');
            let iframe_doc=editor_iframe.contentWindow.document;

            iframe_doc.addEventListener('keydown', check_key);
            document.addEventListener('keydown', check_key);

            function check_key(event){
                if(event.keyCode==13 && iframe_doc.hasFocus()){
                    remove_mark(); } // 改行入力が連続マークとなるのを抑止

                let gate=-1;
                if(event.ctrlKey==true){
                    if(event.keyCode==112){
                        event.preventDefault(); gate=1; }
                    if(gate==1){
                        event.stopImmediatePropagation();
                        do_task(); }}}

            function do_task(){
                if(task==0){
                    caution();
                    task=1;
                    table_panel();
                    enhanced(); }
                else{
                    task=0;
                    remove_t_panel();
                    remove_mark_all(); }}}

        before_end();

    } // catch_key()



    function caution(){
        let disp=
            '<div class="caution_disp">'+
            '<span>'+
            '「Blog Table ⭐」ver.4.0 以前で作成した表を軽量化します。<br>'+
            '表のスタイル指定のためのコードを styleタグに纏める処理で、<br>'+
            '表データを失う事は通常は生じませんが、HTML編集によって<br>'+
            'デザインした表は、デザインの崩れを生じる場合があります。<br>'+
            'そのため、データの多い表・貴重な表を含む記事は、記事を<br>'+
            '複製した上でこのツールを利用する事をお勧めします。<br><br>'+
            'また、軽量化をした表は「Blog Table ⭐」ver.4.0 以降でな <br>'+
            'ないと表の更新ができなくなります。<br>'+
            '</span>'+
            '<input type="button" class="x" value="✖">'+
            '<style>'+
            '.caution_disp { position: absolute; top: 120px; left: calc( 50% - 425px); '+
            'width: 520px; height: auto; font: 18px Meiryo; background: #fff; '+
            'padding: 40px; border: 2px solid #aaa; z-index: 20; }'+
            '.x { position: absolute; top: 8px; right: 9px; padding: 2px 7px 0; }'+
            '</style></div>';

        if(!document.querySelector('.caution_disp')){
            document.body.insertAdjacentHTML('beforeend', disp); }

        let caution_disp=document.querySelector('.caution_disp');
        let x=document.querySelector('.caution_disp .x');
        if(x){
            x.onclick=(()=>{ caution_disp.remove(); }); }}



    function table_panel(){

        let panel=
            '<div id="t_panel">'+
            '<span class="t_label">構成</span>'+
            '<div class="wnc"><input id="col" type="number" min="1"></div>'+
            '<div class="wnr"><input id="row" type="number" min="1"></div>'+
            '<span class="t_label">配置</span>'+
            '<input id="wide" type="submit" value="　">'+
            '<span class="t_label">表幅</span>'+
            '<div class="wpxt"><input id="t_width" type="number" min="10" max="1000"></div>'+
            '<input id="t_width_m" type="submit" value="м">'+
            '<input id="td_padd" type="submit" value="　">'+
            '<input id="equal" type="submit" value="　">'+
            '<span class="t_label">枠線</span>'+
            '<div class="wpx"><input id="border_width" type="number" min="-9"></div>'+
            '<input id="border_color" type="text" autocomplete="off">'+
            '<span class="t_label">最上行背景</span>'+
            '<input id="header_back" type="text" autocomplete="off">'+
            '<span class="t_label">左端列背景</span>'+
            '<input id="left_back" type="text" autocomplete="off">'+
            '<input id="left_back_f" type="submit" value="▲">'+
            '<span class="t_label">全体背景</span>'+
            '<input id="cell_back" type="text" autocomplete="off">'+
            '<span class="t_label">文字</span>'+
            '<div class="wpx"><input id="t_font" type="number" min="12" max="32"></div>'+
            '<input id="set" type="submit" value="　">'+
            '<span id="test"></span>'+

            '<div id="first">'+
            '<span id="bt_help">？</span>'+
            '<div class="bt_help1">'+
            '軽量タイプに変更する表を<b>「Ctrl+左Click」</b>で指定します　　'+
            '<b>「軽量化」</b>以外のボタンは機能しません</div>'+
            '</div>'+

            '<style>'+
            '#t_panel { position: fixed; top: 15px; left: calc(50% - 490px); width: 954px; '+
            'font-size: 14px; padding: 6px 12px; overflow: hidden; '+
            'border: 1px solid #ccc; border-radius: 4px; background: #eff5f6; z-index: 10; }'+
            '#t_panel * { user-select: none; }'+
            '#t_panel input { position: relative; margin-right: 10px; padding-top: 2px; '+
            'height: 27px; box-sizing: border-box; border: thin solid #aaa; }'+
            '#t_panel input[type="number"] { padding-right: 2px; margin-right: 0; }'+
            '#t_panel input[type="number"]:focus, #t_panel input[type="submit"]:focus '+
            '{ box-shadow: none; }'+
            '.t_label { margin: 0 3px 0 0; }'+

            '#col, #row { width: 40px; text-align: center; }'+
            '#wide { width: 30px; letter-spacing: -0.5em; text-indent: -6px; }'+
            '#t_width { width: 54px; text-align: center; }'+
            '#t_width_m { margin-left: -9px; width: 14px; }'+
            '#td_padd { width: 30px; margin-left: 2px; }'+
            '#equal { width: 34px; }'+
            '#border_width { width: 40px; text-align: center; }'+
            '#left_back_f { margin-left: -9px; width: 14px; text-indent: -1px; }'+
            '#t_font { width: 40px; text-align: center; }'+
            '#wide, #t_width_m, #td_padd, #equal, #left_back_f { background: #fff; }'+

            '.wnc, .wnr, .wpx, .wpxt { position: relative; display: inline-block; }'+
            '.wnc { margin-right: 2px; }'+
            '.wnr, .wpx, .wpxt { margin-right: 10px; }'+
            '.wnc::after { content: "列"; }'+
            '.wnr::after { content: "行"; }'+
            '.wpx::after, .wpxt::after { content: "px"; }'+
            '.wnc::after, .wnr::after, .wpx::after, .wpxt::after { position: absolute; right: 2px; '+
            'top: 2px; padding: 3px 0 0; width: 17px; background: #fff; }'+
            '.wpx:hover::after, .wpxt:hover::after, .wnc:hover::after, .wnr:hover::after '+
            '{ content: ""; }'+
            '.wpxt.lock { pointer-events: none; background: #80deea; }'+
            '.wpxt.lock::after { background: inherit; }'+
            '.wpxt.lock #t_width { background: inherit; }'+
            '#t_width_m.lock { pointer-events: none; background: #80deea !important; }'+

            '#border_color { margin-left: -9px; }'+
            '#border_color, #header_back, #left_back, #cell_back { '+
            'width: 0; padding: 2px 16px 0 0; cursor: pointer; }'+
            '#border_color:focus, #header_back:focus, #left_back:focus, #cell_back:focus { '+
            'width: 99px; margin-right: -71px; padding: 2px 0 0 22px; z-index: 1; cursor: text; }'+

            '#set { margin: 0 !important; padding: 2px 12px 0; float: right; font-size: 16px; }'+
            '#set:hover { background: #fff; color: #000; }'+
            '#set { background: #e01919; color: #fff; }'+

            '#first { position: absolute; top: 0; left: 0; color: #fff; background: #2196f3; '+
            'width: 100%; padding: 10px 0; font-size: 16px; text-align: center; }'+
            '#bt_help { position: absolute; top: 11px; right: 25px; padding: 2px 1px 0; '+
            'line-height: 16px; font-weight: bold; border-radius: 30px; '+
            'color: #2196f3; background: #fff; cursor: pointer; }'+
            '.bt_help1 { text-align: left; margin-left: 60px; }'+

            '#test { display: none; }'+
            '#cke_42 { top: 60px !important; left: calc( 50% - 45px) !important; }';

        if(ua==1){
            panel +=
                '.wpx::after, .wpxt::after { padding: 3px 1px 0; }'+
                '.wnc::after { padding: 3px 1px 0; }'+
                '.wnr::after { padding: 3px 1px 0; }'; }

        panel +=
            '</style>'+
            '</div>';

        if(!document.querySelector('#t_panel')){
            document.body.insertAdjacentHTML('beforeend', panel); }

    } // table_panel()



    function enhanced(){
        let target_r=document.getElementById('cke_1_contents'); // 監視 target
        let monitor_r=new MutationObserver(select);
        monitor_r.observe(target_r, {childList: true}); // ショートカット待受け開始

        select();

        function select(){
            if(document.querySelector('.cke_wysiwyg_frame') !=null){ //「通常表示」から実行開始
                remove_mark_all(); // Html編集後のリセット
                show_first(1);
                let editor_iframe=document.querySelector('.cke_wysiwyg_frame');
                let iframe_doc=editor_iframe.contentWindow.document;
                if(iframe_doc){
                    let style_if=
                        '<style id="style_if">'+
                        '.amb_active { box-shadow: #fff -4px 0px, red -8px 0px !important; }'+
                        '</style>';

                    if(!iframe_doc.head.querySelector('#style_if')){
                        iframe_doc.head.insertAdjacentHTML('beforeend', style_if); }

                    let editor=iframe_doc.querySelector('.cke_editable');
                    if(editor){
                        editor.onclick=function(event){
                            event.stopImmediatePropagation();

                            if(event.ctrlKey){
                                remove_mark_all();
                                if(task==1 || task==2 || task==3 || task==4){
                                    let elm=iframe_doc.elementFromPoint(event.clientX, event.clientY);
                                    if(elm.closest('table')!=null){
                                        let table_id=elm.closest('table').id;
                                        if(table_id && table_id.includes('ambt')){
                                            let style_tag=elm.closest('table').previousElementSibling;
                                            if(style_tag && style_tag.classList.contains(table_id)){
                                                remove_mark();
                                                show_first(1);
                                                setTimeout(()=>{
                                                    alert(" ⛔ 選択した表は 軽量タイプの表で 処理の対象ではありません");
                                                },20 ); }
                                            else{
                                                elm.closest('table').parentNode.classList.add('amb_active');
                                                show_first(0);
                                                task=3;
                                                check_available(elm.closest('table'));
                                                edit_table(task, elm.closest('table')); }}}}}} //「表更新」

                    }}}} // select()

    } // enhanced()



    function table_position_set(){
        let wide=document.querySelector('#wide'); // 中央配置・左寄せの設定
        if(posit_set==0){
            wide.value='　▢　';
            table_position='0 auto'; }
        else if(posit_set==1){
            wide.value='▢　　';
            table_position='0 auto 0 0'; }}



    function t_width_lock(r_table){
        let count=0;
        let top_td=r_table.querySelectorAll('tr:first-child td');
        for(let k=0; k<top_td.length; k++){
            if(top_td[k].style.width){
                count+=1; }}
        if(count>0){
            table_lock(1); }
        else{
            table_lock(0); }}


    function table_lock(n){
        let wpxt=document.querySelector('.wpxt'); // 表幅
        let t_width_m=document.querySelector('#t_width_m'); // MEMO
        if(n==0){
            wpxt.classList.remove('lock');
            t_width_m.classList.remove('lock'); }
        else{
            wpxt.classList.add('lock');
            t_width_m.classList.add('lock'); }}



    function td_padding_set(){
        let td_padd=document.querySelector('#td_padd'); // tdの横padding 有無の設定
        if(add_padd=='0'){
            td_padd.value='p0';
            td_padd.style.boxShadow='none'; }
        else{
            td_padd.value='p+';
            td_padd.style.boxShadow='inset 6px 0 0 #cefed0, inset -6px 0 0 #cefed0'; }}



    function lafix_set(task, r_table){
        let equal=document.querySelector('#equal'); // table-layout の設定
        if(layout_fix=='fixed'){
            equal.value='Fix';
            equal.style.background='#80deea'; }
        else{
            layout_fix='auto';
            equal.value='Auto';
            equal.style.background='#fff'; }}



    function table_border_set(){
        let border_width=document.querySelector('#border_width'); // 枠線幅の設定
        two_way();

        function two_way(){
            if(border_width.value>-1){
                border_collapse='collapse';
                table_border_width=0;
                cell_border_width=border_width.value;
                border_space=0; }
            else if(border_width.value<0){
                border_collapse='separate';
                table_border_width=1;
                cell_border_width=1;
                border_space=border_width.value*(-1); }}}



    function left_full_set(){
        let left_back_full=document.querySelector('#left_back_f'); // 左端色を最上行まで設定
        if(left_full==' tr:not(:first-child)'){
            left_back_full.style.color='#aaa';
            left_back_full.style.boxShadow='none'; }
        else{
            left_back_full.style.color='red';
            left_back_full.style.boxShadow='inset 0 5px red'; }}



    function sticky_color(box){
        box.style.boxShadow='inset 17px 0 '+ box.value +', inset 18px 0 #aaa'; }



    function edit_table(task, r_table){
        let editor_iframe=document.querySelector('.cke_wysiwyg_frame');
        let iframe_doc=editor_iframe.contentWindow.document;

        let this_col; // 更新前の列数
        let this_row; // 更新前の行数
        let col=document.querySelector('#col'); // 列数の設定
        let row=document.querySelector('#row'); // 行数の設定
        let wide=document.querySelector('#wide'); // 配置
        let t_width=document.querySelector('#t_width'); // 表全幅の設定
        let t_width_m=document.querySelector('#t_width_m'); // Memo
        let td_padd=document.querySelector('#td_padd'); // Padd
        let equal=document.querySelector('#equal'); // Fix
        let border_width=document.querySelector('#border_width'); // 枠線幅の設定
        let border_color=document.querySelector('#border_color'); // 枠線色の設定
        let header_back=document.querySelector('#header_back'); // 最上行背景色の設定
        let left_back=document.querySelector('#left_back'); // 左端行背景色の設定
        let left_back_f=document.querySelector('#left_back_f');
        let cell_back=document.querySelector('#cell_back'); // 全体背景色の設定
        let t_font=document.querySelector('#t_font'); // 文字サイズの設定
        let set=document.querySelector('#set'); // 作成ボタン

        col.disabled=true;
        row.disabled=true;
        wide.disabled=true;
        t_width.disabled=true;
        t_width_m.disabled=true;
        td_padd.disabled=true;
        equal.disabled=true;
        border_width.disabled=true;
        border_color.disabled=true;
        header_back.disabled=true;
        left_back.disabled=true;
        left_back_f.disabled=true;
        cell_back.disabled=true;
        t_font.disabled=true;

        if(task==3){
            set.value='軽量化';
            table_renew(r_table); }


        function table_renew(r_table){
            t_width_lock(r_table);

            let t_tr=r_table.querySelectorAll('tr');
            row.value=t_tr.length;

            let t_td=r_table.querySelectorAll('td');
            col.value=t_td.length / t_tr.length;

            let margin_g=r_table.style.margin;
            if(margin_g && margin_g.includes('0px auto 0px 0px')){
                posit_set=1; }
            else {
                posit_set=0; }
            table_position_set();

            let t_width_g=r_table.style.width;
            if(t_width_g){
                t_width.value=t_width_g.replace(/[^0-9]/g, ''); }
            else{
                t_width.value=580; }

            let add_padd_g=t_td[t_td.length-1].style.paddingLeft;
            if(add_padd_g){
                add_padd=add_padd_g.slice(0, -2); } // 表末尾の「td」の padding
            else{
                add_padd=0; }
            td_padding_set();

            if(r_table.style.tableLayout=='fixed'){
                layout_fix='fixed'; }
            else{
                layout_fix='auto'; }
            lafix_set(3, r_table);

            let t_border_width_g=t_td[t_td.length-1].style.borderWidth;
            let t_border_width;
            if(t_border_width_g){
                t_border_width=t_border_width_g.replace(/[^0-9]/g, ''); } // 表末尾の「td」の border
            else{
                t_border_width=1; }
            let border_space_g=r_table.style.borderSpacing;
            if(border_space_g){
                border_space=border_space_g.replace(/[^0-9]/g, ''); }
            else{
                border_space=0; }
            if(border_space!=0){
                border_width.value=border_space*(-1); }
            if(border_space==0){
                border_width.value=t_border_width; }
            table_border_set();

            if(t_td[0].style.backgroundColor==''){ // 表先頭「td」の背景色指定の有無
                left_full=' tr:not(:first-child)'; }
            else{
                left_full=' tr'; }
            left_full_set();

            let t_border_color=t_td[t_td.length-1].style.borderColor; // 表末尾の「td」の border色
            if(t_border_color==''){
                t_border_color='#999'; }
            border_color.value=rgb_hex(t_border_color);
            sticky_color(border_color);

            let t_header_back=t_tr[0].style.backgroundColor; // 最初の「tr」の背景色
            if(t_header_back==''){
                t_header_back='#F4F4F4'; }
            header_back.value=rgb_hex(t_header_back);
            sticky_color(header_back);

            let t_left_back;
            if(t_tr.length>1){
                t_left_back=t_td[t_td.length / t_tr.length].style.backgroundColor; // 左端列 背景色 1
                if(t_left_back==''){
                    t_left_back='#F4F4F4'; }}
            else{
                t_left_back=t_td[0].style.backgroundColor; // 左端列 背景色 2
                if(t_left_back==''){
                    t_left_back='#F4F4F4'; }}
            left_back.value=rgb_hex(t_left_back);
            sticky_color(left_back);

            let t_cell_back=r_table.style.backgroundColor; // 表「r_table」の 背景色
            if(t_cell_back==''){
                t_cell_back='#FFF';}
            cell_back.value=rgb_hex(t_cell_back);
            sticky_color(cell_back);

            let t_font_size=r_table.style.fontSize;
            if(t_font_size==''){
                t_font.value='16'; }
            else{
                t_font.value=t_font_size.replace(/[^0-9]/g, ''); }

            let t_word_break=r_table.style.wordBreak;
            if(t_word_break==''){
                word_break='unset'; }
            else{
                word_break=t_word_break; }



            set.onclick=function(){
                if(task==3){
                    let t_tr=r_table.querySelectorAll('tr');
                    this_row=t_tr.length;
                    let t_td=r_table.querySelectorAll('td');
                    this_col=t_td.length / t_tr.length;


                    renew_style(r_table);

                    r_table.removeAttribute('style');
                    let first_tr=r_table.querySelectorAll('tr')[0];
                    if(first_tr){
                        first_tr.removeAttribute('style'); }
                    let top_td=r_table.querySelectorAll('tr:first-child td');
                    top_td[0].style.backgroundColor=''; // コーナーの「td」の背景をリセット
                    for(let k=0; k<top_td.length; k++){
                        top_td[k].style.border='';
                        top_td[k].style.padding='';
                        top_td[k].style.height=''; }
                    let low_td=r_table.querySelectorAll('tr:not(:first-child) td');
                    for(let k=0; k<low_td.length; k++){
                        low_td[k].removeAttribute('style'); }



                    if(layout_fix=='fixed'){ //「Fix」モード時のtable幅適正化
                        let wpxt=document.querySelector('.wpxt'); // 表幅
                        if(!wpxt.classList.contains('lock')){ //「Fix」モードで幅可変
                            let top_td=r_table.querySelectorAll('tr:first-child td');
                            for(let k=0; k<top_td.length; k++){
                                let set_w=getComputedStyle(top_td[k]).width;
                                if(set_w && !top_td[k].style.width){
                                    top_td[k].style.width=set_w; }}}

                        t_width_lock(r_table);

                        t_width.value='';
                        renew_style(r_table);
                        let t_width_g=getComputedStyle(r_table).width;
                        if(t_width_g){
                            t_width.value=Math.ceil((t_width_g.replace('px', ''))); } // 切り上げ
                        else{
                            t_width.value=580; }
                        renew_style(r_table); }



                    setTimeout(()=>{
                        check_available(r_table);
                        alert(" 🟢 軽量化への変換処理を行いました");
                    }, 1000);

                }} // set.onclick()

        } // table_renew()

    } // edit_table()



    function renew_style(r_table){
        let table_id=r_table.id;
        let table_style=r_table.parentElement.querySelector('.'+ table_id);
        if(table_style){
            table_style.textContent=set_css(table_id); }
        else{
            let t_style='<style class="'+ table_id +'">'+ set_css(table_id) +'</style>';
            r_table.insertAdjacentHTML('beforeBegin', t_style); }}


    function set_css(t_id){
        let t_width=document.querySelector('#t_width'); // 表全幅の設定
        let border_color=document.querySelector('#border_color'); // 枠線色の設定
        let header_back=document.querySelector('#header_back'); // 最上行背景色の設定
        let left_back=document.querySelector('#left_back'); // 左端行背景色の設定
        let cell_back=document.querySelector('#cell_back'); // 全体背景色の設定
        let t_font=document.querySelector('#t_font'); // 文字サイズの設定

        return '#'+ t_id + ' { '+
            'width: '+ t_width.value +'px; '+
            'margin: '+ table_position +'; '+
            'table-layout: '+ layout_fix +'; '+
            'border-collapse: '+ border_collapse +'; '+
            'border-spacing: '+ border_space +'px; '+
            'border: '+ table_border_width +'px solid '+ border_color.value +'; '+
            'font: '+ t_font.value +'px Meiryo; '+
            'background-color: '+ cell_back.value +'; '+
            'word-break: '+ word_break +'; } '+
            '#'+ t_id +' tr:first-child { background-color: '+ header_back.value +'; } '+
            '#'+ t_id + left_full +' td:first-child { background-color: '+ left_back.value +'; } '+
            '#'+ t_id +' td { border: '+ cell_border_width +'px solid '+ border_color.value +
            '; padding: 0.2em '+ add_padd +'em 0; height: 1.5em; }'; }



    function remove_t_panel(){
        document.querySelector('#t_panel').remove(); }



    function remove_mark(){
        if(document.querySelector('.cke_wysiwyg_frame') !=null){ //「通常表示」から実行開始
            let editor_iframe=document.querySelector('.cke_wysiwyg_frame');
            let iframe_doc=editor_iframe.contentWindow.document;

            let active_item=iframe_doc.querySelectorAll('.amb_active');
            for(let k=0; k<active_item.length; k++){
                active_item[k].classList.remove('amb_active'); }}}



    function remove_mark_all(){
        remove_mark(); }



    function show_first(n){
        let first=document.querySelector('#first');
        let bt_help1=document.querySelector('.bt_help1');
        if(first){
            if(n==0){
                first.style.display='none'; }
            else{
                first.style.display='block';
                bt_help1.style.display='none';
                if(n==1){
                    bt_help1.style.display='block'; }}}

        let bt_help=document.querySelector('#bt_help');
        if(bt_help){
            bt_help.onclick=function(){
                let url='https://ameblo.jp/personwritep/entry-12838591802.html';
                window.open(url, target="_blank"); }}}



    function check_available(test_table){
        let table_id=test_table.id;
        if(table_id && table_id.includes('ambt')){
            let set=document.querySelector('#set'); // 作成ボタン
            let style_tag=test_table.previousElementSibling;
            if(style_tag && style_tag.classList.contains(table_id)){
                set.style.visibility='hidden'; }
            else{
                set.style.visibility=''; }}}



    function equal_color(R, G, B, A){ // RGBは整数 Aは小数が必須 ➔ 等価 6桁hexコードに変換
        return '#'
            + tohex(upColor(R, A))
            + tohex(upColor(G, A))
            + tohex(upColor(B, A));

        function upColor(value, A){
            let color_value=value*A + 255*(1 - A);
            return Math.floor(color_value); }

        function tohex(value){
            return ('0'+ value.toString(16)).slice(-2); }}



    function hex_bright(hex){ // 明度を段階的に変換
        if(hex.slice(0, 1)=='#'){
            hex=hex.slice(1); }
        if(hex.length==3){
            hex=hex.slice(0,1) + hex.slice(0,1) + hex.slice(1,2) + hex.slice(1,2) +
                hex.slice(2,3) + hex.slice(2,3); }
        // 透過度 0.6 とした色値に変更
        let R=parseInt(hex.slice(0, 2), 16);
        let G=parseInt(hex.slice(2, 4), 16);
        let B=parseInt(hex.slice(4, 6), 16);

        return equal_color(R, G, B, 0.6); } // 非透過色値に変更



    function hex_8_6(hex){ // 8桁hex値を6桁hexに変換
        if(hex.length!=9 || hex.slice(0, 1)!='#'){
            return hex; }
        else{
            hex=hex.slice(1);

            let R=parseInt(hex.slice(0, 2), 16);
            let G=parseInt(hex.slice(2, 4), 16);
            let B=parseInt(hex.slice(4, 6), 16);
            let A=hex.slice(6, 8);
            // 16進の「A値」を透過度（小数）に変更
            let alp=0;
            for(let i=0; i<2; i++){
                alp +=Math.pow(16, -(i + 1))*parseInt(A[i], 16); }

            return equal_color(R, G, B, alp); }} // 非透過色値に変更



    function rgb_hex(color){ // rgb or rgba 表記をhex6桁表記に変換
        if(color.includes('#')){ // hex表記の場合
            return color; }
        else{ // rgb表記の場合
            color=color.split('(')[1].split(')')[0].replace(/ /g, '');
            let rgb_ar=color.split(',');

            let R=parseInt(rgb_ar[0], 10);
            let G=parseInt(rgb_ar[1], 10);
            let B=parseInt(rgb_ar[2], 10);
            let A;
            if(rgb_ar.length==3){
                A=1; }
            else if(rgb_ar.length==4){
                A=parseFloat(rgb_ar[3]); }

            return equal_color(R, G, B, A); }} // 非透過色値に変更



    function before_end(){
        let submitButton=document.querySelectorAll('.js-submitButton');
        submitButton[0].addEventListener('mousedown', all_clear, false);
        submitButton[1].addEventListener('mousedown', all_clear, false);

        function all_clear(){
            let editor_iframe=document.querySelector('.cke_wysiwyg_frame');
            if(!editor_iframe){ //「HTML表示」編集画面の場合
                alert("⛔　Blog Table が処理を終了していません\n\n"+
                      "　　 通常表示画面に戻り 編集を終了してください");
                event.stopImmediatePropagation();
                event.preventDefault(); }
            if(editor_iframe){ //「通常表示」編集画面の場合
                remove_mark_all(); } // table編集・TRIM・COLのマークを削除
        }} // before_end(

} // main()
