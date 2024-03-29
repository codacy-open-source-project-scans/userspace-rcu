# SPDX-FileCopyrightText: 2023 EfficiOS Inc.
#
# SPDX-License-Identifier: MIT

doc_examplesdir = ${docdir}/examples

doc_examples_urcu_flavorsdir = ${doc_examplesdir}/urcu-flavors

dist_doc_examples_urcu_flavors_DATA = \
	urcu-flavors/Makefile \
	urcu-flavors/Makefile.qsbr \
	urcu-flavors/Makefile.mb \
	urcu-flavors/Makefile.membarrier \
	urcu-flavors/Makefile.bp \
	urcu-flavors/qsbr.c \
	urcu-flavors/mb.c \
	urcu-flavors/membarrier.c \
	urcu-flavors/bp.c

dist_doc_examples_DATA = \
	dist-files/Makefile \
	Makefile.examples.template

doc_examples_listdir = ${doc_examplesdir}/list

dist_doc_examples_list_DATA = \
	list/Makefile \
	list/Makefile.cds_list_add_rcu \
	list/Makefile.cds_list_add_tail_rcu \
	list/Makefile.cds_list_del_rcu \
	list/Makefile.cds_list_for_each_rcu \
	list/Makefile.cds_list_for_each_entry_rcu \
	list/Makefile.cds_list_replace_rcu \
	list/cds_list_add_rcu.c \
	list/cds_list_add_tail_rcu.c \
	list/cds_list_del_rcu.c \
	list/cds_list_for_each_rcu.c \
	list/cds_list_for_each_entry_rcu.c \
	list/cds_list_replace_rcu.c

doc_examples_hlistdir = ${doc_examplesdir}/hlist

dist_doc_examples_hlist_DATA = \
	hlist/Makefile \
	hlist/Makefile.cds_hlist_add_head_rcu \
	hlist/Makefile.cds_hlist_del_rcu \
	hlist/Makefile.cds_hlist_for_each_rcu \
	hlist/Makefile.cds_hlist_for_each_entry_rcu \
	hlist/cds_hlist_add_head_rcu.c \
	hlist/cds_hlist_del_rcu.c \
	hlist/cds_hlist_for_each_rcu.c \
	hlist/cds_hlist_for_each_entry_rcu.c

doc_examples_wfcqueuedir = ${doc_examplesdir}/wfcqueue

dist_doc_examples_wfcqueue_DATA = \
	wfcqueue/Makefile \
	wfcqueue/Makefile.cds_wfcq_enqueue \
	wfcqueue/Makefile.cds_wfcq_dequeue \
	wfcqueue/Makefile.cds_wfcq_splice \
	wfcqueue/cds_wfcq_enqueue.c \
	wfcqueue/cds_wfcq_dequeue.c \
	wfcqueue/cds_wfcq_splice.c

doc_examples_wfstackdir = ${doc_examplesdir}/wfstack

dist_doc_examples_wfstack_DATA = \
	wfstack/Makefile \
	wfstack/Makefile.cds_wfs_push \
	wfstack/Makefile.cds_wfs_pop \
	wfstack/Makefile.cds_wfs_pop_all_blocking \
	wfstack/cds_wfs_push.c \
	wfstack/cds_wfs_pop.c \
	wfstack/cds_wfs_pop_all_blocking.c

doc_examples_lfstackdir = ${doc_examplesdir}/lfstack

dist_doc_examples_lfstack_DATA = \
	lfstack/Makefile \
	lfstack/Makefile.cds_lfs_push \
	lfstack/Makefile.cds_lfs_pop_blocking \
	lfstack/Makefile.cds_lfs_pop_all_blocking \
	lfstack/cds_lfs_push.c \
	lfstack/cds_lfs_pop_blocking.c \
	lfstack/cds_lfs_pop_all_blocking.c

doc_examples_rculfqueuedir = ${doc_examplesdir}/rculfqueue

dist_doc_examples_rculfqueue_DATA = \
	rculfqueue/Makefile \
	rculfqueue/Makefile.cds_lfq_enqueue \
	rculfqueue/Makefile.cds_lfq_dequeue \
	rculfqueue/cds_lfq_enqueue.c \
	rculfqueue/cds_lfq_dequeue.c

doc_examples_rculfhashdir = ${doc_examplesdir}/rculfhash

dist_doc_examples_rculfhash_DATA = \
	rculfhash/Makefile \
	rculfhash/jhash.h \
	rculfhash/Makefile.cds_lfht_add \
	rculfhash/Makefile.cds_lfht_add_unique \
	rculfhash/Makefile.cds_lfht_add_replace \
	rculfhash/Makefile.cds_lfht_del \
	rculfhash/Makefile.cds_lfht_destroy \
	rculfhash/Makefile.cds_lfht_lookup \
	rculfhash/Makefile.cds_lfht_for_each_entry_duplicate \
	rculfhash/cds_lfht_add.c \
	rculfhash/cds_lfht_add_unique.c \
	rculfhash/cds_lfht_add_replace.c \
	rculfhash/cds_lfht_del.c \
	rculfhash/cds_lfht_destroy.c \
	rculfhash/cds_lfht_lookup.c \
	rculfhash/cds_lfht_for_each_entry_duplicate.c

# Building the examples requires the shared libraries to be enabled
if ENABLE_EXAMPLES

SUBDIRS_PROXY = hlist list urcu-flavors wfcqueue rculfqueue \
	wfstack lfstack rculfhash

# Copies are for VPATH build support.
all-local:
	$(AM_V_at)if [ x"$(srcdir)" != x"$(builddir)" ]; then \
		cp -pfR $(srcdir)/dist-files $(builddir); \
		chmod -R u+w $(builddir)/dist-files; \
		cp -pf $(srcdir)/Makefile.examples.template $(builddir); \
		chmod u+w $(builddir)/Makefile.examples.template; \
		for subdir in $(SUBDIRS_PROXY); do \
			cp -pfR $(srcdir)/$$subdir $(builddir); \
			chmod -R u+w $(builddir)/$$subdir; \
		done; \
	fi; \
	if [ x"$(shell echo "$(top_srcdir)" | $(GREP) "^/" | wc -l)" = x"1" ]; then \
		rel_src_subdir=""; \
	else \
		rel_src_subdir="../"; \
	fi; \
	if [ x"$(shell echo "$(top_builddir)" | $(GREP) "^/" | wc -l)" = x"1" ]; then \
		rel_build_subdir=""; \
	else \
		rel_build_subdir="../"; \
	fi; \
	$(MAKE) -f dist-files/Makefile CC="$(CC)" CPPFLAGS="$(CPPFLAGS)" AM_CPPFLAGS="$(AM_CPPFLAGS) -I"$${rel_src_subdir}/$(top_srcdir)/include/" -I"$${rel_src_subdir}/$(top_srcdir)/src/" -I"$${rel_build_subdir}$(top_builddir)/include/" -I"$${rel_build_subdir}$(top_builddir)/include/src/"" CFLAGS="$(CFLAGS)" AM_CFLAGS="$(AM_CFLAGS)" LDFLAGS="$(LDFLAGS)" AM_LDFLAGS="$(AM_LDFLAGS) -L../../../src/.libs/ -Wl,-rpath "$(PWD)/../../src/.libs/"" AM_V_P="$(AM_V_P)" AM_V_at="$(AM_V_at)" $(AM_MAKEFLAGS) all;

clean-local:
	$(AM_V_at)$(MAKE) -f dist-files/Makefile $(AM_MAKEFLAGS) clean; \
	if [ x"$(srcdir)" != x"$(builddir)" ]; then \
		for subdir in $(SUBDIRS_PROXY); do \
			rm -rf $(builddir)/$$subdir; \
		done; \
		rm -f $(builddir)/Makefile.examples.template; \
		rm -rf $(builddir)/dist-files; \
	fi;
endif
