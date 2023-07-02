
### Confluence Page
[https://rdbproject.atlassian.net/wiki/spaces/RDBRD/pages/873136162/Traces+How+To](https://rdbproject.atlassian.net/wiki/spaces/RDBRD/pages/873136162/Traces+How+To)
### Build all:
./rebuild.sh gcc Debug

### Run a test:
./Debug/gcc/test/gtest_all/gtest_all --gtest_filter=RowCacheFixture.MS2ComponentTest --gtest_repeat=100

### Open with GDB:
gdb ./Debug/gcc/test/gtest_all/gtest_all -c core.gtest_all.18246.regattavm.localdomain.1688300168

rdb/unit_tests/logs/traces

### Bin to Trace:
./src/tools/traces/open_traces.py -i /tmp/rdb/unit_tests/logs/traces/metadata

### Open with your editor:
/tmp/rdb/unit_tests/logs/traces_out 
