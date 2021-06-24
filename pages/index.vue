<template>
  <div>
      <div class="pt-sm-5" style="margin-top:250px">
          <div class="container">
              <div class="row">
                  <div class="col-lg-12">
                      <div class="text-center">
                          <nuxt-link to="/" class=" d-block auth-logo">
                              <img src="~assets/logoasmart.png" alt height="50px" class="logo logo-dark" />
                          </nuxt-link>

                          <h2 class="mt-3">is coming soon...</h2>
                          <p class="text-muted">
                              Sebuah marketplace untuk membeli sambil bersedekah dengan kerjasama Lembaga Zakat Selangor
                          </p>

                          <div class="row justify-content-center mt-5">
                              <div class="col-lg-10">
                                  <div data-countdown="2020/12/31" class="counter-number">
                                      <div class="coming-box">
                                          {{ days }}
                                          <span>Days</span>
                                      </div>
                                      <div class="coming-box">
                                          {{ hours }}
                                          <span>Hours</span>
                                      </div>
                                      <div class="coming-box">
                                          {{ minutes }}
                                          <span>Minutes</span>
                                      </div>
                                      <div class="coming-box">
                                          {{ seconds }}
                                          <span>Seconds</span>
                                      </div>
                                  </div>
                              </div>
                              <!-- end col-->
                          </div>
                          <!-- end row-->


                      </div>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
/**
 * Coming-soon component
 */
export default {
    data() {
        return {
            title: "Coming-soon",
            start: "",
            end: "",
            interval: "",
            days: "",
            minutes: "",
            hours: "",
            seconds: "",
            starttime: "Nov 5, 2010 15:37:25",
            endtime: "Nov 30, 2021 16:37:25",
        };
    },
    mounted() {
        this.start = new Date(this.starttime).getTime();
        this.end = new Date(this.endtime).getTime();
        // Update the count down every 1 second
        this.timerCount(this.start, this.end);
        this.interval = setInterval(() => {
            this.timerCount(this.start, this.end);
        }, 1000);
    },
    methods: {
        timerCount: function (start, end) {
            // Get todays date and time
            var now = new Date().getTime();

            // Find the distance between now an the count down date
            var distance = start - now;
            var passTime = end - now;

            if (distance < 0 && passTime < 0) {
                clearInterval(this.interval);
                return;
            } else if (distance < 0 && passTime > 0) {
                this.calcTime(passTime);
            } else if (distance > 0 && passTime > 0) {
                this.calcTime(distance);
            }
        },
        calcTime: function (dist) {
            // Time calculations for days, hours, minutes and seconds
            this.days = Math.floor(dist / (1000 * 60 * 60 * 24));
            this.hours = Math.floor(
                (dist % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
            );
            this.minutes = Math.floor((dist % (1000 * 60 * 60)) / (1000 * 60));
            this.seconds = Math.floor((dist % (1000 * 60)) / 1000);
        },
    },
};
</script>

<style scoped>
.counter-number {
  font-size: 28px;
  font-weight: 600;
  text-align: center;
  display: flex;
}

.coming-box {
  width:25%;
}

.counter-number span {
  font-size: 16px;
    font-weight: 400;
    display: block;
    padding-top: 5px
}
</style>