<template>
  <div class="wrapper">
    <div class="card">
      <div v-if="!formSubmitted" class="main-card">
        <div class="img">
          <img src="@/assets/images/icon-star.svg" alt="star svg">
        </div>
        <article>
          <h1>How did we do?</h1>
          <p>
            Please let us know how we did with your support request. All feedback is appreciated 
            to help us improve our offering!
          </p>
        </article>
        <div class="card-form">
          <div class="rating-content">
            <div 
            v-for="(rating , index) in ratingNumber" 
            :key="index" 
            :class="{selected : rating.seleted}"
            @click="selectRate(index)"
            >
              <span>{{ rating.rate }}</span>
            </div>
          </div>
          <button @click="submitRating">Submit</button>
        </div>
      </div>
      <div v-else class="submit-card">
        <img src="@/assets/images/illustration-thank-you.svg" alt="illustration">
        <div class="selected-value">You selected {{ selectedValue }} out of 5</div>
        <h1>Thank you!</h1>
        <p>
          We appreciate you taking the time to give a rating. If you ever need more support, 
          don’t hesitate to get in touch!
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      ratingNumber: [
        {rate: 1 , seleted: false},
        {rate: 2 , seleted: false},
        {rate: 3 , seleted: false},
        {rate: 4 , seleted: false},
        {rate: 5 , seleted: false},
      ],
      selectedValue :null,
      formSubmitted :null, 
    }
  },
  methods: {
    selectRate(index) {
      this.ratingNumber.forEach(rate => rate.seleted = false);
      this.selectedValue = this.ratingNumber[index].rate;
      this.ratingNumber[index].seleted = true;
    },
    submitRating() {
      this.formSubmitted = true;
    },
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Overpass:wght@400;700&display=swap');
  $orange: hsl(25, 97%, 53%);
  $white :hsl(0, 0%, 100%);
  $lightGrey: hsl(217, 12%, 63%);
  $mediumGrey: hsl(216, 12%, 54%);
  $darkBlue: hsl(213, 19%, 18%);
  $veryDarkBlue: hsl(216, 12%, 8%);
  
  * {
    font-family: 'Overpass', sans-serif;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  p {
    font-size: 15px;
  }
  .wrapper {
    width: 100%;
    min-height: 100vh;
    background-color:$veryDarkBlue;
    display: grid;
    place-items: center;
    padding: 1rem;
    .card {
      padding: 2rem;
      background-color: color-mix(in srgb, $darkBlue 40%, $veryDarkBlue 60% ) ;
      color: $white;
      border-radius: 1.5rem;
      max-width: 420px;
      box-shadow: 2px 2px 8px 0px rgba(0, 0, 0, 0.6);
      @media (max-width:560px) {
        padding: 1.5rem;
        border-radius: .5rem;
      }
      .main-card {
        .img {
          width: 40px;
          height: 40px;
          background-color:  $darkBlue;
          display: flex;
          justify-content: center;
          align-items: center;
          opacity: 0.7;
          border-radius: 50%;
          margin-bottom: 1.5rem;
          img {
            max-width: 100%;
            vertical-align: middle;
            height: 14px;
            width: 14px;
          }
        }
        article {
          h1 {
            color: $white;
            line-height: 1;
          }
          p {
            line-height: 1.6;
            margin: 1rem 0 1.5rem;
            color: $mediumGrey;
          }
        }
        .card-form {
          .rating-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
            div {
              width: 50px;
              height: 50px;
              display: flex;
              justify-content: center;
              align-items: center;
              background-color: $darkBlue;
              color: $lightGrey;
              border-radius: 50%;
              font-size: 16px;
              font-weight: 700;
              opacity: 0.8;
              transition: all .2s ease-in-out;
              cursor: pointer;
              &:hover {
                background-color: $orange;
                color: $white;
              }
              &.selected {
                background-color: $lightGrey;
                color: $white;
              }
              span {
                vertical-align: middle;
                line-height: 1;
              }
            }
          }
          button {
            width: 100%;
            padding: .8rem;
            text-transform: uppercase;
            font-size: 1rem;
            background-color: $orange;
            text-align: center;
            vertical-align: middle;
            color: $white;
            border: none;
            border-radius: 2rem;
            font-weight: 700;
            letter-spacing: 1.9px;
            opacity: 0.8;
            cursor: pointer;
            transition: all .15s ease-in-out;
            &:hover {
              background-color: $white;
              color: $orange;
            }
          }
        }
      }
      .submit-card {
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        padding: 0 10px;
        @media (max-width:560px) {
          padding: 0;
        }
        img {
          margin: 1rem 0 2rem;
        }
        div {
          width: fit-content;
          background-color:$darkBlue;
          color: $orange;
          padding: 0.5rem 1rem;
          border-radius: 12px;
          display: flex;
          flex-direction: column;
          justify-content: center;
          line-height: 1;
          align-items: center;
          opacity: .6;
        }
        h1 {
          margin: 1.5rem 0 1rem;
          color: $white;
        }
        p {
          line-height: 1.6;
          color :$lightGrey;
        }
      }
    }
  }
</style>
