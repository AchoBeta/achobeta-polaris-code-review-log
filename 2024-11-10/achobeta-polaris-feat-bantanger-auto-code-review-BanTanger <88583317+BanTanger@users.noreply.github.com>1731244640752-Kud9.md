# Polaris： OpenAi 代码评审.
### 😀代码评分：80
#### 😀代码逻辑与目的：
- `.github/pull-request-template.md` 更新了链接格式，使用相对路径代替绝对路径。
- `.github/workflows/pr_auto_code_review.yml` 添加了一个自动代码评审的工作流程。
- `openai-code-review-sdk-1.0.jar` 添加了一个新的jar文件，用于自动代码评审。
- `IRenderTextService.java` 添加了一个新的注释，描述了一个未实现的文本渲染服务。
- `tag-polaris.sh` 更新了标签生成逻辑，使用相对路径代替绝对路径，并对测试分支的标签进行了更细致的区分。

#### 🤔问题点：
- `.github/pull-request-template.md` 中的链接格式更改可能会导致链接无法正确解析。
- `.github/workflows/pr_auto_code_review.yml` 中使用了未知的jar文件，需要确保其功能正确且安全。
- `IRenderTextService.java` 中注释提到了一个未实现的文本渲染服务，但没有提供实现细节，可能导致误解。
- `tag-polaris.sh` 中的标签生成逻辑可能会在多个分支合并时产生冲突。

#### 🎯修改建议：
- 在 `.github/pull-request-template.md` 中，确保链接使用绝对路径或使用GitHub Pages的完整URL。
- 对 `.github/workflows/pr_auto_code_review.yml` 中的jar文件进行安全性和功能性的验证。
- 在 `IRenderTextService.java` 中提供更详细的实现说明或移除未实现的注释。
- 优化 `tag-polaris.sh` 中的标签生成逻辑，以避免在合并时产生冲突。

#### 💻修改后的代码：
```markdown
diff --git a/.github/pull-request-template.md b/.github/pull-request-template.md
index 759165c..d7cb6cc 100644
--- a/.github/pull-request-template.md
+++ b/.github/pull-request-template.md
@@ -2,7 +2,7 @@
 
 **在提出此拉取请求时，我确认了以下几点（请复选框）：**
 
-- [ ] 我已阅读并理解[贡献者指南]()。
+- [ ] 我已阅读并理解[贡献者指南](https://github.com/your-username/your-repo/README.md)。
 - [ ] 我已检查没有与此请求重复的拉取请求。
 - [ ] 我已经考虑过，并确认这份呈件对其他人很有价值。
 - [ ] 我接受此提交可能不会被使用，并根据维护人员的意愿关闭拉取请求。
diff --git a/.github/workflows/pr_auto_code_review.yml b/.github/workflows/pr_auto_code_review.yml
new file mode 100644
index 0000000..5dfa524
...
```

```markdown
diff --git a/tag-polaris.sh b/tag-polaris.sh
index daaf36d..ba3cdc1 100644
--- a/tag-polaris.sh
+++ b/tag-polaris.sh
@@ -39,8 +39,8 @@ function storage-tag() {
     git pull --tags
     local branch_name=$(echo $(git status | head -1  | awk '{print $NF}'))
     local split_branch_name=${branch_name:0:15}
-    local new_tag=$(echo ${prefix}${split_branch_name}-$(date +'%Y%m%d')-$(git tag -l "${prefix}${split_branch_name}-$(date +'%Y%m%d')-*" | wc -l | xargs printf '%02d'))
+    local new_tag=$(echo ${prefix}${split_branch_name}_$(date +'%Y%m%d')_$(git tag -l "${prefix}${split_branch_name}_$(date +'%Y%m%d')_*" | wc -l | xargs printf '%02d'))
     git tag ${new_tag}
     git push origin $new_tag
 }
```