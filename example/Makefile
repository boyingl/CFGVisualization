#TODO: consider using ant instead of using Makefile to build the example

CFGVisualization=..
ROOT=${CFGVisualization}/..
CHECKERFRAMEWORK=${ROOT}/checker-framework
NULL_CHECKER=org.checkerframework.checker.nullness.NullnessChecker

CHECKER_JAR=${CHECKERFRAMEWORK}/checker/dist/checker.jar
CFGV_CP=${CFGVisualization}/bin
EXAMPLE_BIN=./bin
EXAMPLE_SRC=./src
JAVAC=${CHECKERFRAMEWORK}/checker/bin/javac

all:clean init
	mkdir dotfiles_default
	${JAVAC} -d ${EXAMPLE_BIN} -cp ${CHECKER_JAR} -processor ${NULL_CHECKER} -Acfgviz=org.checkerframework.dataflow.cfg.DOTCFGVisualizer,verbose,outdir=dotfiles_default ${EXAMPLE_SRC}/*.java
	dot -Tpdf dotfiles_default/M-m-Nullness.dot -o pdfs/M-m-Nullness-default.pdf
	make run-dot-TopLevel
	make run-dot-OnlyType
	make run-dot-OnlyBlock
init:
	mkdir ${EXAMPLE_BIN}
	mkdir pdfs

#OnlyBlock,OnlyType,TopLevel
run-dot-%:
	mkdir dotfiles_$*
	${JAVAC} -s ${EXAMPLE_SRC} -d ${EXAMPLE_BIN} -cp ${CHECKER_JAR}:${CFGV_CP} -processor ${NULL_CHECKER} -Acfgviz=DOTCFGVisualizer.DOTCFGVisualizer$*,verbose,outdir=dotfiles_$* ${EXAMPLE_SRC}/*.java
	dot -Tpdf dotfiles_$*/M-m-Nullness.dot -o pdfs/M-m-Nullness-$*.pdf
clean:
	rm -rf pdfs ${EXAMPLE_BIN} dotfiles*