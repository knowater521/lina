<template>
  <Page>
    <ListTable ref="ListTable" :table-config="tableConfig" :header-actions="headerActions" />
  </Page>

</template>

<script>
import ListTable from '@/components/ListTable/index'
import Page from '@/layout/components/Page/index'
import { ActionsFormatter } from '@/components/ListTable/formatters'

export default {
  name: 'DatabaseApp',
  components: {
    ListTable,
    Page
  },
  props: {
  },
  data() {
    return {
      tableConfig: {
        url: `/api/v1/perms/users/database-apps/`,
        columns: [
          {
            prop: 'name',
            align: 'center',
            label: this.$t('assets.Name'),
            sortable: true
          },
          {
            prop: 'get_type_display',
            align: 'center',
            label: this.$t('assets.Type')
          },
          {
            prop: 'database',
            align: 'center',
            label: this.$t('assets.Database')
          },
          {
            prop: 'comment',
            align: 'center',
            showOverflowTooltip: true,
            label: this.$t('assets.Comment')
          },
          {
            prop: 'id',
            align: 'center',
            label: this.$t('assets.Action'),
            formatter: ActionsFormatter,
            formatterArgs: {
              hasDelete: false,
              hasUpdate: false,
              extraActions: [
                {
                  name: 'connect',
                  fa: 'fa-terminal',
                  type: 'primary',
                  callback: function({ row, col, cellValue, reload }) {
                    window.open(`/luna/?type=database_app&login_to=${cellValue}`, '_blank')
                  }
                }
              ]
            }
          }
        ]
      },
      headerActions: {
        hasExport: false,
        hasImport: false,
        hasRefresh: true,
        hasCreate: false,
        hasBulkDelete: false,
        hasBulkUpdate: false,
        hasLeftActions: false,
        hasSearch: true,
        hasRightActions: true
      }
    }
  },
  computed: {

  },
  mounted() {
  },
  methods: {
  }
}
</script>

<style lang='less' scoped>

</style>
