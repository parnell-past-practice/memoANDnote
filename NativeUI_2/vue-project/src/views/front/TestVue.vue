<template>
    <n-radio-group v-model:value="size" name="left-size" style="margin-bottom: 12px">
        <n-radio-button value="small">
            小
        </n-radio-button>
        <n-radio-button value="medium">
            中
        </n-radio-button>
        <n-radio-button value="large">
            大
        </n-radio-button>
    </n-radio-group>
    <n-form ref="formRef" inline :label-width="80" :model="formValue" :rules="rules" :size="size">
        <n-form-item label="姓名" path="name">
            <n-input v-model:value="formValue.name" placeholder="输入姓名" />
        </n-form-item>
        <n-form-item label="年龄" path="age">
            <n-input v-model:value="formValue.age" placeholder="输入年龄" />
        </n-form-item>
        <n-form-item label="电话号码" path="phone">
            <n-input v-model:value="formValue.phone" placeholder="电话号码" />
        </n-form-item>
        <n-form-item>
            <n-button attr-type="button" @click="handleValidateClick">
                验证
            </n-button>
        </n-form-item>
    </n-form>

    <pre>{{ JSON.stringify(formValue, null, 2) }}
</pre>
</template>

<script>
import { defineComponent, ref } from "vue";
import { useMessage } from "naive-ui";

export default defineComponent({
    setup() {
        const formRef = ref(null);
        const message = useMessage();
        window.$message = useMessage();

        return {
            formRef,
            size: ref("medium"),
            formValue: ref({

                name: "",
                age: "",

                phone: ""
            }),
            rules: {
                name: {
                    required: true,
                    message: "请输入姓名",
                    trigger: "blur"
                },
                age: {
                    required: true,
                    message: "请输入年龄",
                    trigger: ["input", "blur"]
                },
                phone: {
                    required: true,
                    message: "请输入电话号码",
                    trigger: ["input"]
                }
            },
            handleValidateClick(e) {
                e.preventDefault();
                formRef.value?.validate((errors) => {
                    if (!errors) {
                        message.success("Valid");
                    } else {
                        console.log(errors);
                        message.error("Invalid");
                    }
                });
            }
        };
    }
});
</script>