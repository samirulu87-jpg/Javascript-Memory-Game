This will include  Comments about important or future usful informtion. 
Link to working site: https://samirulu87-jpg.github.io/Javascript-Memory-Game/


      Style.css colration for the cards 
      * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
      } /*Chenges the defalt padding, margin and box sizing*/
      
      
      body {
          height: 100vh; /* Vh = Viewport, set to 100 it will take 100 percent of the available height*/
          display: flex;
          background-color: #eed13f; 
      }
      
      .memory-game {
          width: 640px;
          height: 640px;
          margin: auto;
          display: flex;
          flex-wrap: wrap;
          perspective: 1000px;
      } /*Chenges the size of the memory card game container*/
      
      .memory-card {
          width: calc(25% - 10px);
          height: calc(33.333% - 10px);
          margin: 5px;
          position: relative;
          transform: scale(1);
          transform-style: preserve-3d;
          transition: transform .5s;
      } /*Changes the size of the card and gives them the postion relative to a parent code */
      
      .memory-card:active {
          transform: scale(.97);
          transition: transform .2s;
      } /* Part of the flippin effect */
      
      .memory-card.flip {
          transform: rotateY(180deg);
      } /* Tells how far or much to flip */
      
      .front-face, .back-face {
          width: 100%;
          height: 100%;
          padding: 20px;
          position: absolute;
          border-radius: 5px;
          background: rgb(255, 230, 214);
          backface-visibility: hidden;
      } /* Changes the size, creates the position and makes it so the backface or the face with the different pictures will be visible when flipped */
      
      .front-face {
          transform: rotateY(180deg)
    }
    Script.js 
    const cards = document.querySelectorAll('.memory-card')

      let hasFlippedCard = false;
      let  lockBoard = false;
      let firstCard, secondCard; 
      
      function flipCard () {
          if (lockBoard) return;
          if (this === firstCard) return;
      
         this.classList.add('flip');
      
         if (!hasFlippedCard) {
          //first click
          hasFlippedCard = true;
          firstCard = this;
      
          return;
      }
      
          //second click
       
          secondCard = this; 
      
      chechForMatch();
      }
      
      
       function chechForMatch() {
          let isMatch = firstCard.dataset.framework === secondCard.dataset.framework
      
          isMatch ? disableCards(): unflipCards();
       }
      
       function disableCards() {
          firstCard.removeEventListener('click', flipCard);
          secondCard.removeEventListener('click', flipCard);
      
              resetBoard()
       }
      
       function unflipCards() {
           lockBoard = true;
      
          setTimeout(() => {
              firstCard.classList.remove('flip');
              secondCard.classList.remove('flip');
      
             resetBoard()
          }, 1500)  
       }
      
      function resetBoard () {
          [hasFlippedCard, lockBoard] = [false, false];
          [firstCard, secondCard] = [null, null];
      }
      
      
      (function shuffle() {
          cards.forEach(card => {
              let randomPos = Math.floor(Math.random() * 12);
              card.style.order = randomPos;
          });
      })();
      
      
      cards.forEach(card => card.addEventListener('click', flipCard));
