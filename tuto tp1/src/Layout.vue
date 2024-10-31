<template>

    <div class="layout">

        <header v-if="$slots.header">
            <slot name="header"></slot>
        </header>

        <aside>
            <slot name="aside"></slot>
        </aside>

        <main>
            <slot name="main"></slot>
        </main>

        <footer>
            <slot name="footer"></slot>
        </footer>

    </div>

</template>


<style></style>