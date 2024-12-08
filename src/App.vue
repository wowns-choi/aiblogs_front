<script>
export default {
  data(){
    return {
      naverUrl : "",
      storeName : "",
    }
  },
  methods: {
    enterUrl(e){
      this.naverUrl = e.target.value; 
      console.log(this.naverUrl);
    },
    enterStoreName(e){
      this.storeName = e.target.value;
      console.log(this.storeName);
    },
    generateWriting() {
      console.log("글 생성");
      fetch('http://localhost:8010/getReviewTitleByGpt',{
        method: 'POST',
        headers: {
          'Content-Type' : 'application/json',
        },
        body: JSON.stringify({
           naverUrl : this.naverUrl,
           storeName : this.storeName,
        })
      })
      .then(response => {
        if (!response.ok){
          throw new Error('Netword response was not ok');
        }
        return response.json();
      })
      .then(data => console.log(data))
      .catch(error => console.error('There has been a problem with your fetch operation:', error))
    }
  }
}


</script>

<template>
  <div class="title">
    AI BLOGS 
  </div>
  <div id="body-container">
    <div class="first-container">
      <input type="text" class="naver-input" placeholder="NAVER URL" @input="enterUrl">
      <button type="button" @click="generateWriting">버튼</button>
    </div>
    <div class="second-container">
      <textarea name="" id="generated-text">

      </textarea>
    </div>
  </div>
</template>

<style scoped>
  #generated-text{
    resize: none; 
    width: 100%; 
    height: 100%;
    /* border-radius: 10px;  */
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    border: 2px solid darkslategray;
    font-size: 18px;
    padding: 0px;
    
  }
  .second-container{
    margin-top: 5vh;
    /* background-color: red; */
    width: 40vw;
    height: 50vh;
    display: flex; 
    justify-content: center;
    align-items: center;
  }
  .naver-input{
    width: 100%;
    height: 5vh;
    /* border-radius: 10px; */
    /* border: 2px solid darkslategray; */
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    border: none;
    padding-left: 30px;
    font-size: 18px;
    outline: none;
    background-color: darkslategray;
    color: #fefefe;
  }
  .naver-input::placeholder {
    font-size: 18px;
    color: #fefefe;


  }
  .first-container{
    width: 25vw;

    margin-top: 5vh;
    background-color: white;


  }
  #body-container{
    /* background-color: darkslategray; */
    height: 100vh;
    display: flex; 
    flex-direction: column;
    align-items: center;
    
  }
  .title{
    height: 20vh;
    display: flex; 
    justify-content: center;
    align-items: center;
    font-size: 50px;
    color: darkslategrey;
    /* border-bottom: 2px solid darkslategray; */
  }
  /* default setting */
  :global(body) {
  display: block; /* flex 대신 기본값으로 변경 */
  place-items: unset;
  background : white;
  color: black;
  }
  :global(#app) {
  display: block; /* grid 대신 block으로 변경 */
  max-width: none;
  padding: 0;
  }
</style>
