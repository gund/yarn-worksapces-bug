# yarn-worksapces-bug

> Repro of the latest Yarn Workspaces bug  
> Issue in Yarn: https://github.com/yarnpkg/berry/issues/2665

## Repro Steps

1. Pull the repo locally
  ```
  git clone git@github.com:gund/yarn-worksapces-bug.git
  ```
2. Navigate to repo
  ```
  cd yarn-worksapces-bug
  ```
3. Run install
  ```
  yarn install
  ```
4. Assert restults

## Assert restults

To assert the issue you need to check root folder `node_modules/@spryker`
as it must contain all the packages hoisted from workspaces packages.

### Actual results (yarn >=v2.4.0)

In the root folder `node_modules/@spryker` there will be just a few packages that are
directly referenced in root `package.json` file and no packages from workspaces packages.

<details>
  <summary>Actual content of the root folder `node_modules/@spryker`:</summary>

```
➜  suite git:(demo-yarn-latest-bug) ls node_modules/@spryker
frontend-config.eslint    frontend-config.stylelint  jquery-query-builder  oryx-for-zed           sql-parser-mistic
frontend-config.prettier  frontend-config.tslint     nestable              sass-resources-loader
```

</details>

### Expected results (yarn <=v2.3.1)

In the root folder `node_modules/@spryker` there should be all packages hoisted from
the workspaces packages as they are all compatible with each other.

<details>
  <summary>Expected content of the root folder `node_modules/@spryker`:</summary>

```
➜  suite git:(demo-yarn-latest-bug) ✗ ls node_modules/@spryker 
ajax-action                                   interception                       table.datasource.http
ajax-action.post-action.close-overlay         jquery-query-builder               table.datasource.inline
ajax-action.post-action.redirect              label                              table.feature.batch-actions
ajax-action.post-action.refresh-drawer        layout                             table.feature.editable
ajax-action.post-action.refresh-parent-table  locale                             table.feature.filters
ajax-action.post-action.refresh-table         logo                               table.feature.pagination
ajax-form                                     modal                              table.feature.row-actions
button                                        navigation                         table.feature.search
card                                          nestable                           table.feature.selectable
checkbox                                      notification                       table.feature.settings
chips                                         oryx-for-zed                       table.feature.sync-state
collapsible                                   pagination                         table.feature.title
data-serializer                               popover                            table.feature.total
date-picker                                   sass-resources-loader              table.filter.date-range
drawer                                        select                             table.filter.select
dropdown                                      sidebar                            table.filter.tree-select
form-item                                     sql-parser-mistic                  tabs
frontend-config.eslint                        styles                             textarea
frontend-config.prettier                      table                              toggle
frontend-config.stylelint                     table.action-handler.form-overlay  tree-select
frontend-config.tslint                        table.action-handler.html-overlay  unsaved-changes
grid                                          table.action-handler.url           unsaved-changes.guard.browser
header                                        table.column.chip                  unsaved-changes.guard.drawer
headline                                      table.column.date                  unsaved-changes.guard.navigation
html-renderer                                 table.column.image                 unsaved-changes.monitor.form
icon                                          table.column.input                 utils
input                                         table.column.select                web-components
input.password                                table.column.text
```

</details>
