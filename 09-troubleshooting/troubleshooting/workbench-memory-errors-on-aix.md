# Workbench memory errors on AIX

If you are running Workbench on AIX and are seeing java memory errors in `mci.log` (there are a few different error messages you may see), and are confident that the machine running Workbench has sufficient memory, you should check the ulimit settings for the AIX user running Workbench. The three ulimit settings worth noting are the Stack, Memory and Data limits.

See the IBM documentation about ulimit settings here:

[https://www.ibm.com/support/knowledgecenter/SS8NLW\_11.0.2/com.ibm.discovery.es.in.doc/iiysiulimits.html](https://www.ibm.com/support/knowledgecenter/SS8NLW_11.0.2/com.ibm.discovery.es.in.doc/iiysiulimits.html)