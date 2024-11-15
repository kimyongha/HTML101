``` html

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>form 유효성 검사</title>
</head>
<body>


<form action="/submit.do" method="post" onsubmit="myValidator(); return false;" class="use_validator">

<fieldset> 
<legend>폼 양식</legend>


<ul>
    <li>input text</li>
    <li><input type="text" name="user_name" title="이름" class="use_vali" placeholder="이름" disabled></li>
</ul>

<ul>
    <li>input checkbox</li>
    <li>
        <label for="">
            <input type="checkbox" name="ott[]" title="ott" value="넷플릭스" class="use_vali"> 넷플릭스
        </label>
        <label for="">
            <input type="checkbox" name="ott[]" title="ott" value="디즈니플러스" class="use_vali"> 디즈니플러스
        </label>
        <label for="">
            <input type="checkbox" name="ott[]" title="ott" value="티빙" class="use_vali"> 티빙
        </label>
        <label for="">
            <input type="checkbox" name="ott[]" title="ott" value="쿠팡플레이" class="use_vali"> 쿠팡플레이
        </label>
        <label for="">
            <input type="checkbox" name="ott[]" title="ott" value="왓챠" class="use_vali"> 왓챠
        </label>
    </li>
</ul>


<ul>
    <li>input radio</li>
    <li>

        <input type="radio" name="gender" value="M" title="성별" class="use_vali">남
        <input type="radio" name="gender" value="F" title="성별" class="use_vali">여
    
    </li>
</ul>

<ul>
    <li>input password</li>
    <li>
        <input type="password" name="passwd" title="비밀번호" class="use_vali">
    </li>
</ul>


<ul>
    <li>textarea</li>
    <li><textarea name="remarks"  title="비고" class="use_vali"></textarea></li>
</ul>

<ul>
    <li>select</li>
    <li>
        <select name="site_list" title="사이트" class="use_vali">
            <option value="">:: 선택 ::</option>
            <option value="네이버">네이버</option>
            <option value="구글">구글</option>
            <option value="다음">다음</option>
        </select>
    </li>
</ul>


<ul>
    <li>취미</li>
    <li>

        <input type="checkbox" name="hobby[]" class="use_vali" title="취미" id="hobby1">
        <label for="hobby1"><span class="custom_inp"></span>독서</label>

        <input type="checkbox" name="hobby[]" class="use_vali" title="취미" id="hobby2">
        <label for="hobby2"><span class="custom_inp"></span>여행</label>

        <input type="checkbox" name="hobby[]" class="use_vali has_etc" title="취미" id="hobby3">
        <label for="hobby3"><span class="custom_inp"></span>기타</label>

        <input type="text" name="hobby_etc" class="use_vali" title="취미 기타" disabled>


    </li>
</ul>

</fieldset>

<input type="submit" value="확인">

</form>    



<script>


// form과 유효성 검사를 할 요소 
let frm = document.querySelector("form.use_validator");
let el = document.querySelectorAll(".use_vali");


// input, select, textarea 유효성검사 
function myValidator(){

    for(let i=0;i<el.length;i++){

        if(el[i].disabled) continue;

        let tagName = el[i].tagName;
        let type = el[i].getAttribute("type");
        let title = el[i].getAttribute("title");
        let name = el[i].getAttribute("name");
        let chkEl = document.getElementsByName(name);

        if(tagName == "INPUT"){

            if(type == "text" || type == "password") {

                if(el[i].value == ""){

                    alert(`${title}을(를) 입력해주세요`);
                    el[i].focus();
                    return false;

                }

            } else if(type == "checkbox" || type == "radio") {
                
                let count = 0;

                for(let j=0;j<chkEl.length;j++){

                    if(chkEl[j].checked) count++;

                }

                if(count < 1){

                    alert(`${title}을(를) 선택해주세요.`);
                    el[i].focus();
                    return false;

                }

            }

        } else if(tagName == "TEXTAREA"){

            if(el[i].value == ""){

                el[i].focus();
                alert(`${title}을(를) 선택해주세요.`);
                return false;

            }

        } else if(tagName == "SELECT"){

            let slctVal = el[i].options[el[i].selectedIndex].value;

            if(slctVal == ""){

                el[i].focus();
                alert(`${title}을(를) 선택해주세요.`);
                return false;

            }

        } 


        

    }

    return true;

}


// 유효성 검사를 사용하는 .use_vali에 대한 클릭 이벤트 
el.forEach(element => {
    element.addEventListener("click", isEtc);
});


// 클릭 이벤트 발생시 추가 인풋에 대한 disabled 처리 
function isEtc(){

    if(!this.classList.contains("has_etc")) return false;

    let name = this.getAttribute("name").replace("[]","");
    let etcEl = document.querySelector(`[name="${name}_etc"]`);

    if (this.checked) {

        etcEl.removeAttribute("disabled");
        etcEl.focus();

    } else {

        etcEl.setAttribute("disabled", true);
        etcEl.value = "";

    }

}


function myValidator_onlyNum(el){
	
   return el.value.replace(/[^0-9]/g,'');
	
}
	
function myValidator_onlyString(el){
	
    return el.value.replace(/[^a-z]/g,'');
     
 }


</script>

    
</body>
</html>


```