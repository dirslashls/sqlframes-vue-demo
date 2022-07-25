<script lang="ts">
import { defineAsyncComponent } from "vue";

const loader = () => {
  return new Promise(async (resolve, reject) => {
    // @ts-ignore
    window.sqlframes_license = {
      data: { domain: "localhost", expiry_date: "2022/09/30" },
      signature:
        "CC1gnQL48/Vlt/RoPYTfKA5KSA191foKpl5mlYLHtj53kpZTIj6pnr4+KYiRmuetkx12HWHNzcBMLsvmt8dv6A==",
    };
    const { default: sfloader } =
      // @ts-ignore
      await import(
        `https://unpkg.com/@sqlframes/repl-app@latest/dist/main.mjs`
      );
    // @ts-ignore
    window.define("monaco-editor", ["vs/editor/editor.main"], (monaco) => {
      monaco.editor.setTheme("vs-dark"); // customize monaco
      return monaco;
    });
    const sf: any = await new Promise((resolve, reject) => {
      sfloader.load(
        "https://unpkg.com/@sqlframes/repl-app@latest/dist/index",
        resolve
      );
    });
    // for autosuggest of the SQL Frames API within the REPL editor
    sf.repl.REPLView.addExtraLibs(
      "https://unpkg.com/@sqlframes/repl-app@latest/dist/api.d.ts",
      "api.d.ts"
    );
    resolve({
      provide: {
        sf: sf,
      },
      render: function () {
        // @ts-ignore
        return this.$slots.default();
      },
    });
  });
};

const SF = defineAsyncComponent<any>({
  loader,
  loadingComponent: { render: () => "Loading..." },
});

export default {
  components: {
    SF,
  },
};
</script>

<template>
  <div class="sf">
    <SF>
      <slot></slot>
    </SF>
  </div>
</template>
