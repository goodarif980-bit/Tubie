<script>

// GAME FLOW CONTROL
let stage = 1;
let score = 0;

// START FIRST GAME
function startGame(){
    stage = 1;
    score = 0;
    game1();
}

// ❤️ GAME 1: Catch Hearts
function game1(){
    document.getElementById("game").innerHTML="Catch 5 hearts ❤️ (0/5)";

    let inter=setInterval(()=>{
        let h=document.createElement("div");
        h.className="heart";
        h.innerHTML="❤️";
        h.style.left=Math.random()*100+"vw";

        h.onclick=()=>{
            h.remove();
            score++;
            document.getElementById("game").innerHTML=`Catch 5 hearts ❤️ (${score}/5)`;

            if(score>=5){
                clearInterval(inter);
                setTimeout(game2,1000);
            }
        };

        document.body.appendChild(h);
        setTimeout(()=>h.remove(),4000);
    },700);
}

// 💔 GAME 2: Avoid Broken Hearts
function game2(){
    document.getElementById("game").innerHTML="Avoid broken hearts 💔 for 5 seconds 😳";

    let alive = true;

    let inter=setInterval(()=>{
        let h=document.createElement("div");
        h.className="heart";
        h.innerHTML="💔";
        h.style.left=Math.random()*100+"vw";

        h.onclick=()=>{
            alive = false;
            clearInterval(inter);
            document.getElementById("game").innerHTML="You touched a broken heart 😢 retrying...";
            setTimeout(game2,1500);
        };

        document.body.appendChild(h);
        setTimeout(()=>h.remove(),3000);
    },500);

    setTimeout(()=>{
        if(alive){
            clearInterval(inter);
            game3();
        }
    },5000);
}

// 🎯 GAME 3: Tap Only ❤️
function game3(){
    document.getElementById("game").innerHTML="Tap only ❤️ (3 correct to win)";

    let correct = 0;

    let inter=setInterval(()=>{
        let emoji = Math.random() > 0.5 ? "❤️" : "😅";

        let e=document.createElement("div");
        e.className="heart";
        e.innerHTML=emoji;
        e.style.left=Math.random()*100+"vw";

        e.onclick=()=>{
            if(emoji==="❤️"){
                correct++;
                if(correct>=3){
                    clearInterval(inter);
                    countdown();
                }
            } else {
                document.getElementById("game").innerHTML="Wrong one 😭 try again...";
                clearInterval(inter);
                setTimeout(game3,1500);
            }
            e.remove();
        };

        document.body.appendChild(e);
        setTimeout(()=>e.remove(),3000);
    },600);
}

</script>
