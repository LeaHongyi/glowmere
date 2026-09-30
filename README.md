# GlowMere listing 实验工作区

用于三个同款、不同主展示色的 Etsy listing 的小规模观察与优化。这里只记录方案和人工核实的数据，不自动修改 Etsy。

## 文件
- `data/listings.csv`：三个链接的当前配置及指定观察窗口的数据。
- `experiments/2026-09-30.md`：首轮计划、基线、观察记录和 edit/copy 判断规则。
- Git 提交保存每轮配置快照；实验文档保存历史窗口，避免覆盖后丢失基线。

## 测试原则
1. 每轮只改一类变量：主图、标题、tags 或价格/折扣。标题与 tags 分轮；价格和折扣属于商业条件，首轮冻结。
2. 改前保存真实 listing ID、完整标题、完整 tags、主图原文件/截图、价格、折扣、全部可选色、库存和配送条件；先提交基线，再提交变更。
3. 默认先改原 listing。没有收藏、没有订单或访问少，不足以支持 copy。
4. 三款颜色、链接年龄及历史流量不同，不能把横向差异视为随机 A/B 结果。以同一链接前后比较为主，未改链接仅提供同期趋势参考。
5. 观察周期提前写定：建议基线和测试各 14 个完整日，覆盖相同星期结构；这是工作约定，不是 Etsy 官方阈值。低流量可预先决定延长到 28 日，并记录原因。
6. 窗口内冻结其他变量；广告、促销、库存、配送、节假日变化均记录。信息错误需立即纠正，标记该窗口受干扰。
7. 未知留空或 TODO；空值不等于 0。只有后台明确为零才填 0。少量访问/订单仅支持方向性观察，不宣布胜出。
8. 到期作出“保留 / 回滚 / 延长 / 无法判断”，不因单日波动连续改动。回滚使用基线配置。

## CSV 口径
每行代表一个真实 listing，A/B/C 只是待映射占位，不是颜色或 Etsy ID；若一个链接含多色，variant 填主展示色，并在实验文档记录完整选项。
- listing_id：Etsy ID，按文本保存；main_image：可追溯文件路径或图片 URL。
- title：完整标题；tags：在一个 CSV 单元格内用分号分隔实际标签。
- price：同一货币下折前标价；discount：折扣百分数，20 表示 20%；货币和多变体价格范围另记实验文档。
- visits / favorites / orders：相同起止时间窗口、相同后台口径的数据，不混用全期累计与窗口新增。若只取得累计收藏，记录起止值与净变化，不能称为新增收藏；若仅有 listing views，不冒充 visits。
- last_changed：实际 Etsy 修改时间，ISO 8601 含时区；未修改留空。建仓日期不是修改日期。
- change_type：实际改动，可用 main_image、title、tags、price_discount；未执行留空。其他类型在实验文档解释。
- CSV 字段有逗号、换行或双引号时按标准 CSV 引号转义。

## 指标与限制
记录原始数，再计算 orders / visits 和窗口收藏 / visits；分母为 0 或口径不匹配则留空。没有曝光量就不能计算点击率；访问变化不直接证明主图提高了点击率。copy 后同时观察原链接、新链接及两者合计，避免只看新链接而忽略流量分流。

## 参考（2026-09-30 查阅）
- [Etsy：编辑 listing](https://help.etsy.com/hc/en-us/articles/115015692667-How-to-Edit-a-Listing)
- [Etsy：批量编辑与复制](https://help.etsy.com/hc/en-us/articles/360000337307-Can-I-Create-or-Edit-Multiple-Listings-at-Once)
- [Etsy：Creating Listings That Convert](https://www.etsy.com/seller-handbook/article/366469719354)：新 listing 有小幅、暂时的搜索提升；不能将初期表现当作持久效果。

以上测试节奏、阈值和 edit/copy 规则是本项目的运营约定，不是平台排名保证。
