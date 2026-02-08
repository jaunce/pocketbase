<script>
    import tooltip from "@/actions/tooltip";
    import CommonHelper from "@/utils/CommonHelper";

    export let date = "";

    let localDate = CommonHelper.formatToLocalDate(date, "yyyy-MM-dd HH:mm:ss.SSS");

    $: dateOnly = localDate ? localDate.substring(0, 10) : null;

    $: timeOnly = localDate ? localDate.substring(10, 19) : null;
    const tooltipData = {
        // generate the tooltip text as getter to speed up the initial load
        // in case the component is used with large number of items
        get text() {
            return date.replace("Z", " UTC");
        },
    };
</script>

{#if date}
    <div class="datetime" use:tooltip={tooltipData}>
        <div class="date">{dateOnly}</div>
        <div class="time">{timeOnly}</div>
    </div>
{:else}
    <span class="txt txt-hint">N/A</span>
{/if}

<style>
    .datetime {
        display: inline-block;
        vertical-align: top;
        white-space: nowrap;
        line-height: var(--smLineHeight);
    }
    .time {
        font-size: var(--smFontSize);
        color: var(--txtHintColor);
    }
</style>
