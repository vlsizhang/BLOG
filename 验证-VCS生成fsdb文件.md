a.testbench
加入波形生成语句
initial begin    
$fsdbDumpfile("tb.fsdb");
$fsdbDumpvars;
end
b.仿真脚本
加入verdi接口库的路径
#!/bin/csh -f
setenv NOVAS_HOME  /user/EDA_Tools/Synopsys/verdi3-I-201403-SP1setenv NOVAS_PLI ${NOVAS_HOME}/share/PLI/VCS/LINUX64setenv LD_LIBRARY_PATH $NOVAS_PLI
setenv NOVAS  "${NOVAS_HOME}/share/PLI/VCS/LINUX64"
setenv novas_args  "-P $NOVAS/novas.tab   $NOVAS/pli.a "
vcs +v2k -sverilog +vcs+lic+wait -full64 -debug_pp \
+warn=noCDNYI,noIPDW,noILLGO,noTMR,noPHNE,noIRIID-W \
-Mupdate +notimingcheck +nospecify \
${novas_args}\       
-f file.f \
./simv
c.Verdi调试
verdi -f file.f -ssf tb.fsdb &
