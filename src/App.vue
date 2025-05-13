<template>
  <div id="container">
    <h1>GAME</h1>
    <div id="bot-placeholder">
      <img :src="botImage">
    </div>
    <div id="you-placeholder">
      <img :src="playerImage">
    </div>
    <div id="buttons-container">
      <div id="btn-paper" @click="handleSelect(1)"></div>
      <div id="btn-scissor" @click="handleSelect(2)"></div>
      <div id="btn-rock" @click="handleSelect(3)"></div>
    </div>
  </div>
</template>
 
<script>
export default {
  name: 'App',
  data() {
    return {
      botChoice: 0,
      playerChoice: 0,
      winner: null, // bot, player, null
    }
  },
  methods: {
    handleSelect(index) {
      this.playerChoice = index;

      // generate a choice for the bot
      this.botChoice = Math.ceil(Math.random() * 3);

      if (this.botChoice === this.playerChoice) {
        this.winner = null;
      } else if (
        (this.playerChoice === 1 && this.botChoice === 3) ||
        (this.playerChoice === 2 && this.botChoice === 1) ||
        (this.playerChoice === 3 && this.botChoice === 2)
      ) {
        this.winner = 'player';
      } else {
        this.winner = 'bot';
      }
    },
    translateChoice(index) {
      const choices = {};
      choices[1] = 'paper';
      choices[2] = 'scissor';
      choices[3] = 'rock';

      return choices[index];
    },
  },
  computed: {
    botImage() {
      if (this.botChoice !== 0 && this.playerChoice !== 0) {
        const choice = this.translateChoice(this.botChoice);
        let result;
        if (this.winner == null) result = 'draw';
        if (this.winner === 'bot') result = 'win';
        if (this.winner === 'player') result = 'lose';

        return `/images/${choice}-${result}.png`;
      }

      return '/images/Placeholder-Bot.png';
    },
    playerImage() {
      if (this.botChoice !== 0 && this.playerChoice !== 0) {
        const choice = this.translateChoice(this.playerChoice);
        let result;
        if (this.winner == null) result = 'draw';
        if (this.winner === 'bot') result = 'lose';
        if (this.winner === 'player') result = 'win';

        return `/images/${choice}-${result}.png`;
      }

      return '/images/Placeholder-You.png';
    },
  },
}
</script>
 
<style>
#container {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100vh;
  padding-top: 40px;
  box-sizing: border-box;
  background-color: #44D7B6;
}
 
#bot-placeholder, #you-placeholder {
  flex: 0px 2 1;
}
 
#bot-placeholder img, #you-placeholder img {
  display: block;
  width: 60%;
  height: auto;
  margin: auto;
}
 
#buttons-container {
  flex: 0px 1 1;
  display: flex;
  flex-direction: row;
}
 
#buttons-container div {
  flex: 0px 1 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center bottom;
}
 
#buttons-container div#btn-paper {
  background-image: url('/public/images/paper-btn.png');
}
 
#buttons-container div#btn-scissor {
  background-image: url('/public/images/scissor-btn.png');
}
 
#buttons-container div#btn-rock {
  background-image: url('/public/images/rock-btn.png');
}

h1 {
  background-color: #000;
  color: #fff;
  text-align: center;
  margin-top: -40px;
}
</style>