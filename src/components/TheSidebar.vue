<template>
  <aside
    class="hidden xl:block w-64 max-h-screen overflow-auto fixed top-0 pt-12 bg-white z-20"
  >
    <SidebarSection>
      <ul>
        <SidebarNavItem label="Home" icon="home" isActive />
        <SidebarNavItem label="Trending" icon="fire" />
        <SidebarNavItem label="Subscriptions" icon="subscriptions" />
      </ul>
    </SidebarSection>
    <SidebarSection>
      <ul>
        <SidebarNavItem label="Library" icon="duplicate" />
        <SidebarNavItem label="History" icon="time" /></ul
    ></SidebarSection>
    <SidebarSection class="px-8 py-4 font-medium leading-5 border-b">
      <span class="text-sm">
        Sign in to like videos, comment, and subscribe.
      </span>
      <ButtonLogin
        class="focus:outline-none flex items-center px-2 py-0.5 mt-3 text-sm text-blue-700 uppercase border border-blue-700 rounded-sm"
      />
    </SidebarSection>
    <SidebarSection>
      <SidebarSectionHeading title="Best of YouTube" />
      <ul>
        <SidebarNavItem label="Music" icon="music" />
        <SidebarNavItem label="Sports" icon="sport" />
        <SidebarNavItem label="Gaming" icon="game" />
        <SidebarNavItem label="Movies" icon="movies" />
        <SidebarNavItem label="News" icon="news" />
        <SidebarNavItem label="Live" icon="live" />
        <SidebarNavItem label="360&deg; Video" icon="video360" />
      </ul>
    </SidebarSection>
    <SidebarSection>
      <ul>
        <SidebarNavItem label="Browse channels" icon="channels" />
      </ul>
    </SidebarSection>
    <SidebarSection>
      <SidebarSectionHeading title="More from YouTube" />
      <ul>
        <SidebarNavItem label="YouTube Premium" icon="premium" />
        <SidebarNavItem label="Live" icon="live" />
      </ul>
    </SidebarSection>
    <SidebarSection>
      <ul>
        <SidebarNavItem label="Settings" icon="settings" />
        <SidebarNavItem label="Report history" icon="report" />
        <SidebarNavItem label="Help" icon="questionMark" />
        <SidebarNavItem label="Send feedback" icon="message" />
      </ul>
    </SidebarSection>
    <SidebarSection class="px-6 py-4 text-xs font-semibold space-y-4">
      <TheFooter />
    </SidebarSection>
  </aside>
</template>

<script>
import SidebarNavItem from './SidebarNavItem.vue';
import ButtonLogin from './ButtonLogin.vue';
import SidebarSectionHeading from './SidebarSectionHeading.vue';
import SidebarSection from './SidebarSection.vue';
import TheFooter from './TheFooter.vue';
export default {
  name: 'TheSidebar',
  components: {
    TheFooter,
    SidebarSection,
    SidebarSectionHeading,
    ButtonLogin,
    SidebarNavItem,
  },
};
</script>

<style scoped></style>
