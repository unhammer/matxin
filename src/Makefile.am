EXTRA_DIST = config.h data_manager.h matxin_string_utils.h simpleregex.h string_utils.h utf_converter.h xml_reader.h gen_fst2regex.sh gen_matxin_translator.sh deformat.xsl txt-format.xml wiki-format.xml rtf-format.xml html-format.xml

bin_PROGRAMS = matxin-analyser matxin-xfer-lex matxin-xfer-intra matxin-xfer-inter matxin-xfer-adp \
	       matxin-xfer-verb matxin-gen-inter matxin-gen-intra matxin-gen-move \
	       matxin-gen-morf matxin-reformat matxin-destxt matxin-deswiki matxin-deshtml matxin-desrtf

bin_SCRIPTS = matxin fst2regex.pl

matxin_analyser_SOURCES = analyser.cc io_redirect_handler.cc io_redirect_handler.hpp
matxin_analyser_LDADD = -lfreeling -lboost_system -lboost_program_options

matxin_xfer_lex_SOURCES = lex_trans.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_xfer_lex_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_xfer_intra_SOURCES = st_intra.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_xfer_intra_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_xfer_inter_SOURCES = st_inter.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_xfer_inter_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_xfer_adp_SOURCES = st_prep.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_xfer_adp_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_xfer_verb_SOURCES = st_verb.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_xfer_verb_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_gen_inter_SOURCES = sg_inter.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_gen_inter_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_gen_intra_SOURCES = sg_intra.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_gen_intra_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_gen_move_SOURCES = sg_move.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_gen_move_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_gen_morf_SOURCES = morph_gen.cc data_manager.cc utf_converter.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_gen_morf_LDADD = -lfreeling -lfoma -lboost_system -lboost_program_options

matxin_reformat_SOURCES = reformat.cc utf_converter.cc data_manager.cc xml_reader.cc simpleregex.cc matxin_string_utils.cc matxin_string_utils.h io_redirect_handler.cc io_redirect_handler.hpp
matxin_reformat_LDADD = -lfoma

matxin_destxt_SOURCES = txt-deformat.cc
matxin_deswiki_SOURCES = wiki-deformat.cc
matxin_deshtml_SOURCES = html-deformat.cc
matxin_desrtf_SOURCES = rtf-deformat.cc

txt-deformat.cc: txt-format.xml Makefile.am deformat.xsl
	$(XSLTPROC) --stringparam mode matxin deformat.xsl txt-format.xml | $(FLEX) -Cfer -t >$@

wiki-deformat.cc: wiki-format.xml Makefile.am deformat.xsl
	$(XSLTPROC) --stringparam mode matxin deformat.xsl wiki-format.xml | $(FLEX) -Cfer -t >$@

html-deformat.cc: html-format.xml Makefile.am deformat.xsl
	$(XSLTPROC) --stringparam mode matxin deformat.xsl html-format.xml | $(FLEX) -Cfer -t >$@

rtf-deformat.cc: rtf-format.xml Makefile.am deformat.xsl
	$(XSLTPROC) --stringparam mode matxin deformat.xsl rtf-format.xml | $(FLEX) -Cfer -t >$@

matxin: Makefile.am gen_matxin_translator.sh
	@echo "Creating $@ script"
	@echo "#!$(BASH)" > $@
	@echo "MATXIN_DIR=\"$(prefix)\"" >> $@
	@cat gen_matxin_translator.sh >> $@
	@chmod a+x $@

fst2regex.pl: Makefile.am gen_fst2regex.sh
	@echo "Creating $@ script"
	@echo "#!$(PERL)" > $@
	@cat gen_fst2regex.sh >> $@
	@chmod a+x $@
