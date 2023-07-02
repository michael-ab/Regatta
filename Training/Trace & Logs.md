
### Build all:
./rebuild.sh gcc Debug

Run a test:
./Debug/gcc/test/gtest_all/gtest_all --gtest_filter=RowCacheFixture.MS2ComponentTest --gtest_repeat=100

Open with GDB:
gdb ./Debug/gcc/test/gtest_all/gtest_all -c core.gtest_all.18246.regattavm.localdomain.1688300168

rdb/unit_tests/logs/traces

BIN TO TRACE:
./src/tools/traces/open_traces.py -i /tmp/rdb/unit_tests/logs/traces/metadata

OPEN TRACES WITH EDITOR:
/tmp/rdb/unit_tests/logs/traces_out 
