---
title: xadmin 简单配置记录
date: 2016-07-17 14:59:02
categories: python
tags: 
    - python
    - django
    - xadmin
---
## 公共配置
``` bash
class BaseSetting(object):
    #开启主题选择
    enable_themes = True
    use_bootswatch = True
xadmin.site.register(views.BaseAdminView, BaseSetting)

class GlobalSetting(object):
    #全局检索model
    global_search_models = [Boy, ]
    #model对应icon
    global_models_icon = {
        Boy: 'fa fa-laptop',
    }
    #菜单导航栏样式 accordion 和 default
    menu_style = 'accordion'#'accordion'
    site_title=u'站点标题'
    site_footer=u'公司'
    #菜单导航配置实例
    def get_site_menu(self):
        return (
            {'title': '内容管理', 'perm': self.get_model_perm( Boy, 'change'), 'menus':(
                {'title': '游戏资料', 'icon': 'info-sign', 'url': self.get_model_url(Boy, 'changelist')},
                {'title': '组', 'icon': 'info-sign', 'url': self.get_model_url(Group, 'changelist')},
                {'title': '全县', 'icon': 'info-sign', 'url': self.get_model_url(Permission, 'changelist')},
                {'title': '用户', 'icon': 'info-sign', 'url': self.get_model_url(User, 'changelist')},
                {'title': '网站文章', 'icon': 'file', 'url': self.get_model_url(Boy, 'changelist') + '?_rel_categories__id__exact=1'},
            )},
            {'title': '分类管理', 'perm': self.get_model_perm(Boy, 'change'), 'menus':(
                {'title': '主要分类', 'url': self.get_model_url(Boy, 'changelist') + '?_p_parent__isnull=True'},
                {'title': '游戏资料', 'url': self.get_model_url(Boy, 'changelist') + '?_rel_parent__id__exact=2'},
            )},

        )
xadmin.site.register(views.CommAdminView, GlobalSetting)
```
## model配置
``` bash
class DemoModelAdmin(object):
    #展示字段diy
    def open_web(self, instance):
        return "<a href='http://%s' target='_blank'>Open</a>" % instance.name
    open_web.short_description = "Acts"
    open_web.allow_tags = True
    open_web.is_column = True
    app_label=u'当前model名称'
    #列表页展示内容
    list_display=('name','age','like','home','birthday','is_new','open_web','y')
    #列表页链接字段
    list_display_links = ('age',)
    #列表页顶部过滤器
    list_filter=('age','birthday','is_new',('like',xadmin.filters.MultiSelectFieldListFilter))
    #列表页顶部搜索
    search_fields=('name','age')
    list_quick_filter = ['like', {'field': 'name', 'limit': 10}]
    #列表页细节展示
    show_detail_fields=('name',)
    #列表页单字段编辑
    list_editable=('birthday','is_new','y')
    batch_fields=('contact','age')
    relfield_style = 'fk-ajax'
    #删除还原
    reversion_enable = True
    #add新条目时的分步操作
    wizard_form_list = [
        ('First\'s Form', ('name', )),
        ('Second Form', ('birthday',)),
        ('Thread Form', ('age',))
    ]
    #自动刷新设置
    refresh_times = (3, 5, 10)
    actions = None
    #列表页底部统计
    aggregate_fields = {"age": "sum"}
    #列表页可选布局
    grid_layouts = ('table', 'thumbnails')
    #书签
    list_bookmarks = [{'title': "Need Guarantee", 'query': {'age__exact': 16}, 'order': ('-age',),
                       'cols': ('name', 'birthday',)}]
    #详情页布局                       
    form_layout = (
        Main(
            TabHolder(
                Tab('Comm Fields',
                    Fieldset('Company data',
                             'name', 'age',
                             description="some comm fields, required"
                             ),
                    # Inline(MaintainLog),
                    ),
                Tab('Extend Fields',
                    Fieldset('Contact details',
                             'name',
                             Row('name', 'like'),
                             Row('name', 'birthday'),
                             Row(AppendedText(
                                 'like', 'G'), AppendedText('name', "G")),
                             'birthday'
                             ),
                    ),
            ),
        ),
        Side(
            Fieldset('Status data',
                     'age', 'like', 'birthday'
                     ),
        )
    )
    #图表绘制
    data_charts = {
        u"aa1": {'title': u"统计表", "x-field": "age", "y-field": ("y","birthday"),"order":('age',)},
        u"aa2": {'title': u"统表", "x-field": "age", "y-field": "birthday", "order": ('age',)},
        "per_month": {'title': u"Monthly Users", "x-field": "_chart_month", "y-field": ("y",),"order":("age",),
                      "option": {
                          "series": {"bars": {"align": "center", "barWidth": 0.1, 'show': True}},
                          "xaxis": {"aggregate": "sum", "mode": "categories"},
                      },
                      },
    }
    def _chart_month(self,obj):
        return obj.birthday.strftime("%m")


xadmin.site.register(Demomodel,DemoModelAdmin)
```
