<template>
    <div class="card basic-data-table radius-12 overflow-hidden">
        <div class="card-body p-0">
            <!-- Editor Toolbar Start -->
            <div id="toolbar-container">
                <span class="ql-formats">
                    <select class="ql-font"></select>
                    <select class="ql-size"></select>
                </span>
                <span class="ql-formats">
                    <button class="ql-bold"></button>
                    <button class="ql-italic"></button>
                    <button class="ql-underline"></button>
                    <button class="ql-strike"></button>
                </span>
                <span class="ql-formats">
                    <select class="ql-color"></select>
                    <select class="ql-background"></select>
                </span>
                <span class="ql-formats">
                    <button class="ql-script" value="sub"></button>
                    <button class="ql-script" value="super"></button>
                </span>
                <span class="ql-formats">
                    <button class="ql-header" value="1"></button>
                    <button class="ql-header" value="2"></button>
                    <button class="ql-blockquote"></button>
                    <button class="ql-code-block"></button>
                </span>
                <span class="ql-formats">
                    <button class="ql-list" value="ordered"></button>
                    <button class="ql-list" value="bullet"></button>
                    <button class="ql-indent" value="-1"></button>
                    <button class="ql-indent" value="+1"></button>
                </span>
                <span class="ql-formats">
                    <button class="ql-direction" value="rtl"></button>
                    <select class="ql-align"></select>
                </span>
                <span class="ql-formats">
                    <button class="ql-link"></button>
                    <button class="ql-image"></button>
                    <button class="ql-video"></button>
                    <button class="ql-formula"></button>
                </span>
                <span class="ql-formats">
                    <button class="ql-clean"></button>
                </span>
            </div>

            <!-- Editor Start -->
            <div id="editor">
                <p>This policy explains how 6amMart website and related applications (the “Site”, “we” or “us”)
                    collects, uses, shares and protects the personal information that we collect through this site or
                    different channels. 6amMart has established the site to link up the users</p>
                <p><br /></p>

                <h6>Using ChatGPT</h6>
                <p>This policy explains how 6amMart website and related applications (the “Site”, “we” or “us”)
                    collects, uses, shares and protects the personal information that we collect through this site or
                    different channels. 6amMart has established the site to link up the users who need foods or grocery
                    items to be shipped or</p>
                <p><br /></p>

                <h6>Intellectual Property</h6>
                <p>This policy explains how 6amMart website and related applications (the “Site”, “we” or “us”)
                    collects, uses, shares and protects the personal information that we collect through this site or
                    different channels. 6amMart has established the site to link up the users who need foods or grocery
                    items to be shipped or delivered by the riders from the affiliated restaurants or shops to the
                    desired location. This policy also applies to any mobile applications that we develop for use</p>
                <p><br /></p>

                <h6>Using ChatGPT</h6>
                <p>This policy explains how 6amMart website and related applications (the “Site”, “we” or “us”)
                    collects, uses, shares and protects the personal information that we collect through this site or
                    different channels. 6amMart has established the site to link up the users who need foods or grocery
                    items to be shipped or delivered by the riders from the affiliated restaurants or shops to the
                    desired location. This policy also applies to any mobile applications that we develop for use with
                </p>
                <p><br /></p>

                <p>our services on the Site, and references to this “Site”, “we” or “us” is intended . grocery items to
                    be shipped or delivered by the riders from the affiliated restaurants or shops to the desired
                    location. This policy also applies to any mobile applications that we develop for use</p>

                <p>Some initial <strong>bold</strong> text</p>
                <p><br /></p>
            </div>

        </div>

        <div class="card-footer p-24 bg-base border border-bottom-0 border-end-0 border-start-0">
            <div class="d-flex align-items-center justify-content-center gap-3">
                <button type="button"
                    class="border border-danger-600 bg-hover-danger-200 text-danger-600 text-md px-50 py-11 radius-8"
                    @click="cancel">
                    Cancel
                </button>
                <button type="button" class="btn btn-primary border border-primary-600 text-md px-28 py-12 radius-8"
                    @click="saveContent">
                    Save Changes
                </button>
            </div>
        </div>
    </div>
</template>

<script>
import Quill from "quill";
import { onMounted } from "vue";

export default {
    name: "TermsCondition",
    setup() {
        onMounted(() => {
            new Quill("#editor", {
                modules: {
                    toolbar: "#toolbar-container",
                },
                theme: "snow",
                placeholder: "Compose an epic...",
            });
        });

        const cancel = () => {
            console.log("Cancelled");
        };

        const saveContent = () => {
            const editorContent = document.querySelector('#editor .ql-editor')?.innerHTML;
            console.log("Saved Content:", editorContent);
        };

        return {
            cancel,
            saveContent,
        };
    },
};
</script>