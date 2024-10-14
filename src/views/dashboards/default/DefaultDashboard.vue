<script lang="ts">
// imported components
import ChartCards from '@/views/widgets/chart/components/ChartCards.vue';
import RepeatCustomer from '@/views/widgets/chart/components/RepeatCustomer.vue';
import ProjectOverview from '@/views/widgets/chart/components/ProjectOverview.vue';
import UserCard from '@/views/widgets/statistics/components/UserCard.vue';
import ProjectCard from './components/ProjectCard.vue';
import TransactionCard from '@/views/widgets/data/components/TransactionCard.vue';
import TotalIncome from '@/views/widgets/chart/components/TotalIncome.vue';
import OnboardingModal from '@/views/dashboards/default/components/OnboardingModal.vue'

export default {
  name: 'DefaultDashboard',
  components: {
    ChartCards,
    RepeatCustomer,
    ProjectOverview,
    UserCard,
    ProjectCard,
    TransactionCard,
    TotalIncome,
    OnboardingModal,
  },
  data() {
    return {
      showOnboardingModal: true
    };
  },
  methods: {
    closeOnboardingModal(): void {
      document.documentElement.style.overflow = 'auto'
      this.showOnboardingModal = false
    }
  }
}
</script>

<template>
  <!-- -------------------------------------------------------------------- -->
  <!-- Chart widgets -->
  <!-- -------------------------------------------------------------------- -->
  <ChartCards />

  <v-row class="mb-0">
    <v-col cols="12" xl="9" md="8">
      <v-row>
        <!-- -------------------------------------------------------------------- -->
        <!-- Repeat customer -->
        <!-- -------------------------------------------------------------------- -->
        <v-col cols="12">
          <RepeatCustomer />
        </v-col>

        <!-- -------------------------------------------------------------------- -->
        <!-- Project overview -->
        <!-- -------------------------------------------------------------------- -->
        <v-col cols="12">
          <ProjectOverview />
        </v-col>
      </v-row>
    </v-col>

    <v-col cols="12" xl="3" md="4">
      <v-row>
        <!-- -------------------------------------------------------------------- -->
        <!-- Project -->
        <!-- -------------------------------------------------------------------- -->
        <v-col cols="12">
          <ProjectCard />
        </v-col>

        <!-- -------------------------------------------------------------------- -->
        <!-- User card -->
        <!-- -------------------------------------------------------------------- -->
        <v-col cols="12">
          <UserCard />
        </v-col>
      </v-row>
    </v-col>
  </v-row>

  <v-row>
    <!-- -------------------------------------------------------------------- -->
    <!-- Transactions -->
    <!-- -------------------------------------------------------------------- -->
    <v-col cols="12" md="6">
      <TransactionCard />
    </v-col>

    <!-- -------------------------------------------------------------------- -->
    <!-- Total income -->
    <!-- -------------------------------------------------------------------- -->
    <v-col cols="12" md="6">
      <TotalIncome />
    </v-col>
  </v-row>
  <OnboardingModal v-if="showOnboardingModal" @onboarding-completed="closeOnboardingModal()"></OnboardingModal>
</template>
