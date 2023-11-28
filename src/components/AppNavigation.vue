<template>
  <div
    class="sidebar border border-right col-md-3 col-lg-2 p-0 bg-body-tertiary"
  >
    <div
      class="offcanvas-md offcanvas-end bg-body-tertiary"
      tabindex="-1"
      id="sidebarMenu"
      aria-labelledby="sidebarMenuLabel"
    >
      <div class="offcanvas-header">
        <h5 class="offcanvas-title" id="sidebarMenuLabel">Company name</h5>
        <button
          type="button"
          class="btn-close"
          data-bs-dismiss="offcanvas"
          data-bs-target="#sidebarMenu"
          aria-label="Close"
        ></button>
      </div>
      <nav
        class="offcanvas-body d-md-flex flex-column p-0 pt-lg-3 overflow-y-auto"
      >
        <ul class="nav flex-column">
          <li class="nav-item" v-for="item in items" :key="item.title">
            <router-link :to="item.href" class="nav-link"
              ><span data-bs-target="#sidebarMenu" data-bs-dismiss="offcanvas"
                ><i :class="item.icon"></i> {{ item.title }}</span
              ></router-link
            >
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppNavigation",
  data() {
    return {
      appTitle: "Parrot Hub",
      items: [
        { title: "Home", href: "/", icon: "bi bi-house" },
        {
          title: "Location",
          href: "/location",
          icon: "bi bi-geo-alt",
        },
        { title: "Hub", href: "/hub", icon: "bi bi-modem" },
        {
          title: "Devices",
          href: "/devices",
          icon: "bi bi-boxes",
        },
        { title: "SmartApps", href: "/isas", icon: "bi bi-gear" },
        {
          title: "Integrations",
          href: "/integrations",
          icon: "bi bi-diagram-3",
        },
        { title: "Settings", href: "/settings", icon: "bi bi-sliders" },
        {
          title: "SmartApp Code",
          href: "/sa-code",
          icon: "bi bi-file-earmark-text",
        },
        {
          title: "Device Handler Code",
          href: "/dh-code",
          icon: "bi bi-file-earmark-text",
        },
        {
          title: "Extensions",
          href: "/extensions",
          icon: "bi bi-puzzle",
        },
      ],
    };
  },
};
</script>

<style scoped></style>
