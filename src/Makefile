RAGEL=ragel
PARSERS=seq/fasta/parser.jl \
		seq/fastq/parser.jl \
		intervals/bed/parser.jl \
		intervals/bigbed/parser.jl \
		align/hts/sam/parser.jl

all: $(PARSERS)

clean:
	rm -f $(PARSERS)

%.jl: %.rl
	$(RAGEL) -Y --goto-backend -G2 $< -o $@.tmp
	echo "# WARNING: This file was generated from $< using ragel. Do not edit!" > $@
	sed 's/[[:space:]]*$$//g' $@.tmp >> $@
	rm $@.tmp

%.dot: %.rl
	$(RAGEL) -p -V $< > $@

%.svg: %.dot
	dot -Tsvg < $< > $@
