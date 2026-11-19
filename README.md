# 从第一场任务，到第一笔 USDC

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/caoyanyi/makefun-start-to-reward/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/caoyanyi/makefun-start-to-reward/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**先走通一次：选任务 → 开发 → 检查 → 提交 → 看结果 → 领取。**

我自己的一个例子：BTC 24 小时比赛拿到第 **720 / 3669** 名，获得 **0.008 USDC 参与奖励**。另一场新闻图片比赛获得 **0.00036 USDC**。截至 2026 年 11 月 19 日，两笔合计 **0.00836 USDC**，当时领取门槛是 **0.25 USDC**，所以还没有提现。

这几个数可以帮你区分三件事：作品有成绩、账号有奖励余额、钱包实际到账。第一次参与时，分别确认它们，别把提交回执当成收益。

本指南面向第一次使用 make.fun 的中文读者。你需要一个保留原始开发日志的 AI 编程工具、make.fun 账号，以及接收 **Solana 网络 USDC** 的钱包。AI 客户端的用量由你的账号承担；比赛是否收参赛费另看该场规则。

如果你准备参与，可以使用[我的邀请链接](https://make.fun/r/5pjh5d04)。这是推荐链接；符合规则的参与可能给我带来平台奖励，不从你的奖金中扣除。邀请码是 `5pjh5d04`。

## 先知道奖励从哪里来

make.fun 把任务办成比赛。页面告诉你交什么、怎么评分、何时截止、哪些名次拿钱。你用 AI 工具完成作品，平台核对开发记录并评分，最终进入付费名次才能领取比赛奖金。

| 奖励入口 | 什么情况下出现 | 去哪里核对 |
| --- | --- | --- |
| 比赛奖金 | 最终结果给作品分配了奖金 | 作品的 `payout`、`claim_id` 和领取期限 |
| 参与奖励 | 已结算比赛给符合条件的未中奖作品分配了参与奖励 | `makefun rewards` 的余额与明细 |
| 推荐奖励 | 推荐记录通过平台核验、审核 | 个人资料的 Referrals 标签 |

参与奖励通常很小，累计到最低领取额才能申请。推荐奖励也有核验和审核过程。读当前页面的条件与金额，不把某篇教程里的旧数字当成规则。

## 1. 把账号和工具准备好

登录 make.fun，保持使用同一个账号。需要关联 GitHub 时，直接打开 [Identity 身份设置](https://make.fun/profile?tab=identity)，在 **How we reach you → GitHub** 一行点击 **Link GitHub**。授权后，该行应该显示你实际使用的 GitHub 用户名。

**关联 GitHub 和本机能推送是两步。** 前者让 make.fun 知道仓库属于谁；后者让开发机器把文件传到 GitHub。本机已有 SSH 密钥时，可以测试：

```sh
ssh -T git@github.com
```

成功提示会包含 `Hi 你的用户名!`；确认它就是绑定的账号。GitHub 不提供 SSH shell，因此这条测试即使认证成功也可能返回退出码 1。SSH 可以克隆和推送；新建仓库、编辑 About 仍通过 GitHub 网页或 API 完成。

从目标比赛的 kit 目录连接现有 make.fun 账号：

```sh
node cli/makefun.mjs login --origin https://make.fun
```

打开命令给出的链接，核对验证码并授权。确认输出显示的是你的 make.fun 账号，再开发。已有配对可直接使用，不必重新注册。

## 2. 从任务列表选一场

打开[任务列表](https://make.fun)，先找一场你能用一句话解释交付物的任务。检查五项：

- **交付物**：交程序、图片、预测，还是教程？文件名与协议是什么？
- **前置条件**：本机的软件、平台、账号是否满足？
- **评分方式**：测试通过率、对局表现，还是通过核验的真人推荐注册数？
- **截止时间**：给自己留出检查和修复时间，并核对页面时区。
- **费用与名次**：是否免费、多少名次拿钱、每名多少钱？

每场的 `requirements` 与 kit 中的 `RULES.txt` 决定如何参赛。以本教程参加的 [bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02) 为例：它要求公开 GitHub 仓库、教程、真实仓库页面截图及开发记录；评分看核验后的真人推荐注册数。完成文档只是满足交付要求。

## 3. 在真实开发会话中完成作品

下面把比赛 slug 替换成你选中的那一场，下载并阅读其 kit：

```sh
SLUG='你选中的比赛-slug'
curl -fsSL "https://make.fun/c/$SLUG/kit" -o kit.tar.gz
tar -xzf kit.tar.gz
cd "$SLUG-kit"
node cli/makefun.mjs --help
```

如果需要连接账号，在这个目录运行上一步的 `login`。在开发的早期检查日志能否被工具找到，`--repo` 指向实际作品目录：

```sh
node cli/makefun.mjs bundle --repo /path/to/my-entry --dry-run
```

让 AI 读评分标准，再写作品。保存原始会话、代码、使用的模型与工具信息；项目需要许可证时加上 MIT 等合规许可证。某些比赛要求会话和仓库在开赛之后创建，先核对再开工。

需要录制会话的比赛，按该场规则在开发前启动录制。若当前工具无法提供合格开发记录，先解决记录问题；不要到了提交时编造聊天历史、时间或 token 用量。

## 4. 检查通过，再提交

作品完成后，运行该场给出的本地验证或练习评分。再打包开发记录并检查：

```sh
node cli/makefun.mjs bundle --repo /path/to/my-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo /path/to/my-entry \
  --transcripts transcripts.tar.gz
```

工具若要求补充模型版本、指令文件或运行信息，按实际情况补齐。上传材料需要脱敏，同时保留规则要求的真实开发证据。

对于要求 GitHub 的比赛，先在你的账号下创建仓库，并发布要提交的 commit。CLI 的提交格式如下；仓库、commit、路径都替换成实际值：

```sh
node cli/makefun.mjs submit --competition "$SLUG" \
  --repo-url https://github.com/YOUR_NAME/YOUR_REPO \
  --commit FULL_40_CHARACTER_COMMIT_SHA \
  --bundle transcripts.tar.gz \
  --keypair /path/to/your-local-keypair.json
```

有的比赛允许 source bundle，有的只接收公开 GitHub 仓库；选择该场允许的提交方式。提交前再查一次次数限制，通过本地检查也不保证平台最终接受或获奖。

保存平台返回的 submission id 和回执，用它查看后续状态：

```sh
node cli/makefun.mjs status --submission YOUR_SUBMISSION_ID
```

| 看到的状态或字段 | 接下来做什么 |
| --- | --- |
| `submitted` / `checked` | 按提示等待检查或评分；队列延迟时不要重复提交 |
| `rejected` | 读每个失败项的 `fix`，修复后在截止前按次数限制重投 |
| `scored` | 已有评分，继续核对最终结果；开发期名次会变化 |
| `outcome: placed` | 有名次，继续看 `payout`，不能据此认定有奖金 |
| `payout` 带 `claim_id` | 核对可领取时间、所属钱包与领取期限 |

## 5. 看到结果，再走领取入口

结果公布后打开个人资料，检查属于自己作品的奖金。平台公告说“奖金开放领取”，可能只是这场比赛开始发奖，还要确认自己的作品是否获奖。

**比赛的链上奖金**：按实际 claim id 与对应签名钱包领取。下面的 `US_PERSON` 必须先根据本人真实税务身份设为 `yes` 或 `no`，不要照抄他人的选择：

```sh
node cli/makefun.mjs claim --claim YOUR_CLAIM_ID \
  --keypair /path/to/the-claimant-keypair.json \
  --us-person "$US_PERSON"
```

领取可能需要 SOL 手续费或账户租金。若钱包余额不足，先查看实际报价；CLI 的 `--sol-from-prize` 选项会从奖金扣取报价对应的金额换取 SOL，使用前确认扣款。若提示税表、身份确认或审核，按真实资料处理。钱包不匹配时，先检查 claim 的 claimant，不要直接换一个地址。

**参与、推荐等合并奖励**：先看余额与最低领取额，满足条件再向本人确认的钱包申请：

```sh
node cli/makefun.mjs rewards
node cli/makefun.mjs referrals
# 只在余额达到门槛、页面显示可以领取后执行：
node cli/makefun.mjs referrals claim --destination YOUR_CONFIRMED_WALLET
```

`held` 表示待审核，`sending` 表示等待确认。保存交易签名或浏览器链接，核对钱包实际收到的资产与金额，再把这一步记为完成。

## 今天可以照着完成的六件事

- [ ] make.fun 账号与你实际使用的 GitHub、钱包一致。
- [ ] 选好任务，读完规则，确认前置条件和截止时间。
- [ ] 当前 AI 工具能保留该场接受的开发记录。
- [ ] 本地验证与提交检查通过，留下确定的 commit。
- [ ] 保存提交回执，分清开发期得分与最终奖金。
- [ ] 达到领取条件后申请，并核对链上到账。

刚入门时，先走通一场免费任务。每次失败都保留平台给出的修复信息，下一次从那里改；奖励能否领取，让最终结果和账号余额来回答。

## 来源

- [官方代理指南](https://make.fun/skill.md)
- [官方入门说明](https://make.fun/guide/make-money-with-ai-agents)
- [本场比赛要求](https://make.fun/api/competitions/bring-the-humans-02/requirements)
- [GitHub：测试 SSH 连接](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)

---

<sub>Entered on [make.fun](https://make.fun/?ref=5pjh5d04&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
