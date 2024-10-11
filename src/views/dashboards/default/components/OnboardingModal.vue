<template>
    <div class="main-container">
      <div class="backdrop">
        <div class="onboarding-container">
          <div class="steps">
            <div
              v-for="(step, index) in steps"
              :key="index"
              :class="['step-child', currentStep >= index + 1 ? 'active' : '']"
            ></div>
          </div>
          <div class="onboarding-header">
            <h3 style="font-weight: 600">
              Step {{ currentStep }}: {{ steps[currentStep - 1].title }}
            </h3>
            <p style="font-size: 13px;">{{ steps[currentStep - 1].description }}</p>
          </div>
          <div class="dynamic-content-container">
            <transition :name="swipeDirection" mode="out-in">
              <div
                class="step-container"
                v-if="currentStep == 1"
                key="main-content"
              >
                <div class="account-card-container">
                  <div
                    v-for="account in accounts"
                    :key="account.id"
                    :class="[
                      'account-card',
                      account.id == accountSelected ? 'selected' : '',
                    ]"
                    @click="toggleSelection(account.id)"
                  >
                    <div class="account-card-body">
                      <h3 class="account-card-title">
                        {{ account.title }}
                      </h3>
                      <div class="account-card-content">
                        <ul class="account-card-benefits">
                          <li v-for="benefit in account.benefits" :key="benefit">
                            {{ benefit }}
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div v-else-if="currentStep == 2" key="personal-information">
                <div class="onboarding-form-container">
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>First name:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.firstName"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>Last name:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.lastName"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="12" cols="12" class="pb-md-3 pb-1">
                      <v-label>Email address:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.email"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>Title:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.title"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>Phone number:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.phone"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="12" cols="12" class="pb-md-3 pb-1">
                      <v-label>Linkedin:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.linkedin"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>Country:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.country"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>State:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.state"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>City:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="personalInformation.city"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                </div>
              </div>
              <div v-else-if="currentStep == 3" key="company-information">
                <div>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="12" cols="12" class="pb-md-3 pb-1">
                      <v-label>Company name:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="companyInformation.name"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="12" cols="12" class="pb-md-3 pb-1">
                      <v-label>Address:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="companyInformation.address"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>State:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="companyInformation.state"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>City:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="companyInformation.city"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>Zip code:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="companyInformation.zipcode"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                    <v-col md="6" cols="12" class="pb-md-3 pb-1">
                      <v-label>Company size:</v-label>
                      <v-select
                        :items="['1 to 10', '11 to 25', '26+']"
                        role="link"
                        color="primary"
                        variant="outlined"
                        hide-details
                        density="comfortable"
                        v-model="companyInformation.size"
                      ></v-select>
                    </v-col>
                  </v-row>
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="12" cols="12" class="pb-md-3 pb-1">
                      <v-label>Website:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="companyInformation.website"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                  </v-row>
                </div>
              </div>
              <div v-else-if="currentStep == 4" key="dsp-information">
                <div v-for="(dsp, index) in dsps" :key="index">
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="5" cols="5" class="pb-md-3 pb-1">
                      <v-label>DSP:</v-label>
                      <v-select
                        :items="['Dv360', 'Pulsepoint', 'The trade desk', 'Basis']"
                        role="link"
                        color="primary"
                        variant="outlined"
                        hide-details
                        density="comfortable"
                        v-model="dsp.dsp"
                      ></v-select>
                    </v-col>
                    <v-col md="5" cols="5" class="pb-md-3 pb-1">
                      <v-label>Seat ID:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="dsp.seatId"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                    <v-col md="2" cols="2" class="pb-md-3 pb-1 remove-btn" @click="removeDSP(index)">
                      <v-icon icon="$trashCanOutline"></v-icon>
                    </v-col>
                  </v-row>
                </div>
                <div style="width: fit-content; margin: 20px auto">
                  <div class="add-dsp" @click="addDSP">New DSP</div>
                </div>
              </div>
              <div v-else-if="currentStep == 5" key="advertisers-information">
                <div v-for="(advertiser, index) in advertisers" :key="index">
                  <v-row class="mb-md-n3 mb-n1">
                    <v-col md="5" cols="5" class="pb-md-3 pb-1">
                      <v-label>Name:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="advertiser.name"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                    <v-col md="5" cols="5" class="pb-md-3 pb-1">
                      <v-label>Brand URL:</v-label>
                      <v-text-field
                        variant="outlined"
                        density="comfortable"
                        v-model="advertiser.url"
                        single-line
                        hide-details
                        color="primary">
                      </v-text-field>
                    </v-col>
                    <v-col md="2" cols="2" class="pb-md-3 pb-1 remove-btn" @click="removeDSP(index)">
                      <v-icon icon="$trashCanOutline"></v-icon>
                    </v-col>
                  </v-row>
                </div>
                <div style="width: fit-content; margin: 20px auto">
                  <div class="add-advertiser" @click="addAdvertiser">
                    New Advertiser
                  </div>
                </div>
              </div>
            </transition>
          </div>
          <div class="onboarding-footer">
            <div class="action-btn-container">
              <span
                v-if="currentStep > 1"
                class="action-btn-back"
                @click="handlePrevious"
              >
                <v-icon icon="$chevronLeft"></v-icon><span>PREVIOUS</span>
            </span>
              <div style="width: inherit"></div>
              <v-col cols="3" sm="3">
                <v-btn
                  color="primary"
                  variant="flat"
                  rounded="md"
                  block
                  :disabled="nextButtonDisabled"
                  @click="handleNext"
                >
                  {{ nextButtonLabel }}
                </v-btn>
              </v-col>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>

  <script>

  export default {
    name: 'OnboardingModal',
    props: {
      onFinish: {
        type: Function,
        required: true
      }
    },
    data() {
      return {
        accounts: [
          {
            id: 1,
            title: 'Trader',
            benefits: [
              'Unlimited PMP creation',
              'Fast and easy menu',
              'Connect to your DSP Fast',
              'texto de prueba, lo que se lee aqui no va en el diseño original.',
            ],
            color: '#234a75',
          },
          {
            id: 2,
            title: 'Reseller',
            benefits: [
              'Unlimited PMP creation',
              'Fast and easy menu',
              'Connect to your DSP Fast',
              'texto de prueba, lo que se lee aqui no va en el diseño original.',
            ],
            color: '#035db8',
          },
          {
            id: 3,
            title: 'Vendor',
            benefits: [
              'Unlimited PMP creation',
              'Fast and easy menu',
              'Connect to your DSP Fast',
              'texto de prueba, lo que se lee aqui no va en el diseño original.',
            ],
            color: '#2c5c8e',
          },
        ],
        accountSelected: 0,
        showMainContent: true,
        currentStep: 1,
        personalInformation: {
          firstName: '',
          lastName: '',
          email: '',
          phone: '',
          title: '',
          country: '',
          state: '',
          city: '',
          linkedin: '',
        },
        companyInformation: {
          companyName: '',
          address: '',
          state: '',
          city: '',
          zipcode: '',
          website: '',
          size: '',
        },
        dsps: [{ dsp: '', seatId: '' }],
        advertisers: [{ name: '', url: '' }],
        swipeDirection: 'swipe-left',
      }
    },
    computed: {
      nextButtonLabel() {
        return this.currentStep > 4 ? 'FINISH' : 'NEXT'
      },
      nextButtonDisabled() {
        if (this.currentStep == 1) {
          return !this.accountSelected
        } else {
          return false
        }
      },
      availableDSPs() {
        return [
          'Select your DSP',
          {
            value: 'dv360',
            label: 'Dv360',
          },
          {
            value: 'pulsepoint',
            label: 'Pulsepoint',
          },
          {
            value: 'tradedesk',
            label: 'The trade desk',
          },
          {
            value: 'basis',
            label: 'Basis',
          },
        ]
      },
      sizeOptions() {
        return [
          {
            id: 1,
            name: '1 to 10',
          },
          {
            id: 2,
            name: '11 to 26',
          },
          {
            id: 3,
            name: '26 or more',
          },
        ]
      },
      steps() {
        return [
          {
            title: 'Account type',
            description: 'Select your account type to continue',
          },
          {
            title: 'Personal information',
            description: 'Enter your personal information',
          },
          {
            title: 'Company information',
            description: 'Enter your company information',
          },
          {
            title: 'DSPs information',
            description: 'Enter your DSPs information',
          },
          {
            title: 'Advertisers information',
            description: 'Enter your advertisers information',
          },
        ]
      },
    },
    emits: ['onboarding-completed'],
    methods: {
      removeDSP(index) {
        this.dsps.splice(index, 1)
      },
      removeAdvertiser(index) {
        this.advertisers.splice(index, 1)
      },
      toggleSelection(accountId) {
        this.accountSelected = accountId
      },
      handleNext() {
        this.swipeDirection = 'swipe-left'
        switch (this.currentStep) {
          case 1:
            this.currentStep = 2
            break
          case 2:
            this.currentStep = 3
            break
          case 3:
            this.currentStep = 4
            break
          case 4:
            this.currentStep = 5
            break
          case 5:
            this.$emit('onboarding-completed');
        }
      },
      handlePrevious() {
        this.swipeDirection = 'swipe-right'
        switch (this.currentStep) {
          case 2:
            this.currentStep = 1
            break
          case 3:
            this.currentStep = 2
            break
          case 4:
            this.currentStep = 3
            break
          case 5:
            this.currentStep = 4
            break
        }
      },
      moveToStep(step) {
        if (step > this.currentStep) {
          this.swipeDirection = 'swipe-left'
          this.currentStep = step
        } else if (step < this.currentStep) {
          this.swipeDirection = 'swipe-right'
          this.currentStep = step
        }
      },
      addDSP() {
        this.dsps.push({ dsp: '', seatId: '' })
      },
      addAdvertiser() {
        this.advertisers.push({ name: '', url: '' })
      },
    },
  }
  </script>
  
  <style scoped>
  .main-container {
    display: flex;
    height: 100vh;
    width: 100vw;
    max-height: 100vh;
    max-width: 100vw;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1500;
  }
  
  .backdrop {
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.75);
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  
  .steps {
    width: 100%;
    height: 5px;
    display: flex;
    margin-bottom: 20px;
  }
  
  .step-child {
    flex-grow: 1;
    margin-right: 5px;
    background-color: lightgray;
    border-radius: 5px;
  }
  
  .step-child:last-child {
    margin-right: 0px;
  }
  
  .step-child.active {
    background-color: rgb(var(--v-theme-primary));;
  }
  
  .image-container {
    background-color: rgb(var(--v-theme-primary));;
    width: -webkit-fill-available;
    height: 100vh;
    z-index: 999;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .onboarding-container {
    width: 40%;
    min-width: 600px;
    margin-left: 0;
    height: fit-content;
    padding: 25px;
    background-color: rgb(var(--v-theme-containerBg));
    border-radius: 12px;
  }

  .onboarding-header {
    margin-bottom: 20px;
  }

  .step-container {
    width: 100%;
  }

  .account-card {
    cursor: pointer;
    width: 100%;
    margin-bottom: 15px;
    border-radius: 5px;
    transition: margin-top 0.2s ease;
    border: 3px solid transparent;
    background-color: rgb(var(--v-theme-background));
    padding: 20px;
  }
  
  .account-card:hover {
    border: 3px solid rgb(var(--v-theme-primary));;
    cursor: pointer;
  }
  
  .account-card.selected {
    background-color: #0d71fd0d;
    border: 3px solid rgb(var(--v-theme-primary));;
  }
  
  .account-card-title {
    font-weight: 600;
    margin-bottom: 6px;
  }
  
  .account-card-benefits {
    padding-left: 14px;
    font-size: 13px;
  }
  
  .account-card-footer {
    width: 100%;
  }
  
  .account-card-button {
    padding: 8px;
    width: 150px;
    text-align: center;
    margin: auto;
    border-radius: 35px;
    font-size: 15px;
    background-color: rgb(var(--v-theme-primary));;
    color: white;
  }
  
  .account-card-button:hover {
    cursor: pointer;
    /* background-color: #035db8; */
  }
  
  .account-card-learn-more {
    text-align: center;
    margin: 4px auto;
    font-size: 10px;
  }
  
  .actions {
    display: flex;
    width: calc(100vw);
    padding: 1rem 4rem;
    padding-left: 20rem;
    position: fixed;
    bottom: 0;
    right: 0;
    background-color: rgb(var(--v-theme-primary));;
    display: none;
  }
  
  .actions-right {
    width: fit-content;
    display: flex;
    flex-direction: row-reverse;
    width: 90px;
  }
  
  .actions-left {
    width: fit-content;
    display: flex;
    width: 90px;
  }
  
  .actions-center {
    color: white;
    width: -webkit-fill-available;
  }
  
  .action-btn-container {
    width: 100%;
    display: flex;
    margin: 40px auto 20px auto;
  }
  
  .action-btn {
    background-color: rgb(var(--v-theme-primary));;
    color: white;
    border: 2px solid rgb(var(--v-theme-primary));;
    min-width: 90px;
    border-radius: 7px;
    font-weight: 500;
  }
  
  .action-btn:hover {
    color: rgb(var(--v-theme-primary));;
    background-color: white;
  }
  
  /* .action-btn:hover {
    background-color: #041e41;
  } */
  
  .action-btn-back {
    font-weight: 400;
    color: grey;
    margin: 20px 0;
    cursor: pointer;
    font-size: 13px;
    display: flex;
  }
  
  .actions-steps {
    width: fit-content;
    margin: 7px auto;
  }
  
  .step-description-separator {
    margin: 0 10px;
  }
  
  .step-description {
    color: white;
    font-size: 14px;
    font-weight: 200;
    cursor: pointer;
  }
  
  .step-description.active {
    font-size: 16px;
    font-weight: 600;
    cursor: default;
  }
  
  .add-icon-container {
    width: 30px;
    height: 30px;
    text-align: center;
    font-weight: 400;
    border: 1px solid grey;
    border-radius: 7px;
    padding-top: 4px;
    margin: auto;
    color: grey;
    background-color: white;
    cursor: pointer;
  }
  
  .add-advertiser {
    text-decoration: underline;
    color: grey;
    margin: 9px;
    cursor: pointer;
  }
  
  .add-dsp {
    text-decoration: underline;
    color: grey;
    margin: 9px;
    cursor: pointer;
  }
  
  .remove-btn {
    width: 40px;
    flex: none;
    height: 40px;
    bottom: 0;
    position: relative;
    text-align: center;
    cursor: pointer !important;
    font-weight: 600;
    padding: 47px 33px;
  }
  
  .remove-btn:hover {
    color: rgba(var(--v-theme-error), var(--v-medium-opacity));
  }
  
  .swipe-left-enter-active,
  .swipe-left-leave-active {
    transition:
      transform 0.2s ease,
      opacity 0.2s ease;
  }
  
  /* Starting state of the entering element (off-screen to the right) */
  .swipe-left-enter {
    transform: translateX(5%);
    opacity: 0; /* Start with opacity 0 */
  }
  
  /* Final state for the leaving element (off-screen to the left) */
  .swipe-left-leave-to {
    transform: translateX(-5%);
    opacity: 0; /* Fade out */
  }
  
  /* Initial state of the leaving element (on-screen) */
  .swipe-left-leave {
    transform: translateX(0);
    opacity: 1;
  }
  
  .swipe-right-enter-active,
  .swipe-right-leave-active {
    transition:
      transform 0.2s ease,
      opacity 0.2s ease;
  }
  
  /* Starting state of the entering element (off-screen to the right) */
  .swipe-right-enter {
    transform: translateX(-5%);
    opacity: 0; /* Start with opacity 0 */
  }
  
  /* Final state for the leaving element (off-screen to the left) */
  .swipe-right-leave-to {
    transform: translateX(5%);
    opacity: 0; /* Fade out */
  }
  
  /* Initial state of the leaving element (on-screen) */
  .swipe-right-leave {
    transform: translateX(0);
    opacity: 1;
  }
  
  .flex {
    display: flex;
  }
  
  @media (max-width: 700px) {
    .image-container {
      display: none;
    }
  
    .onboarding-container {
      width: 100vw;
      height: 100vh;
      min-width: 0px;
      border-radius: 0;
      max-height: 100vh;
    }
  
    .onboarding-container {
      padding: 25px;
    }
  
    .action-btn:hover {
      background-color: rgb(var(--v-theme-primary));;
      color: white;
    }
  }
  
  ::v-deep .form-control {
    height: 40px;
    font-size: 14px;
  }
  
  ::v-deep .form-label {
    margin-top: 18px !important;
    margin-bottom: 5px !important;
  }
  
  ::v-deep .form-select {
    height: 40px;
    font-size: 14px;
  }
  
  ::v-deep .card-body {
    padding: 15px 20px;
  }
  </style>
  