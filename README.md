## （例）TALE.pdbをMDする場合

# /pdb

gmxtool/pdb フォルダ内に任意の.pdbファイルを入れる ※複数個に対応


# 実行
$ bash gmx.sh
(capecod : >qsub gmx.sh)


# /.

初回にTALE①、log②、rmsd③フォルダがgmxtool内に追加される


# /TALE　①

MDされる.pdbのファイル名が実行フォルダになり、直下にMD結果が出力される


# /log　②

実行済みpdbファイルがlogフォルダに移される


# /rmsd　③

クリーニング済みのrmsdデータが出力される


# パラメータ調整

gmx.sh
#------------------
box="2.0"
ion1="K"
ion2="CL"
gpu="01"
mpi="1"
omp="8"
#$ -pe ompi 8
#$ -q allquincy.q
#$ -N hoge0
#------------------
	〜
	〜

上記に以下のパラメータを入力する
gpu	：プロセス数以下のgpuidを指定
mpi	：プロセス並列数
omp	：スレッド並列数
-pe ompi：使用コア数（=mpi×omp）
-q	：UGEに登録されているクラスタ名(allcapecod.q  allquincy.q  allessex.q  allweymouth.q)
-N	：Job名


# MD後のディレクトリ階層の一例

TALE.pdb
├── TALE_rmsd.xvg  
├── em
│   ├── em.edr
│   ├── em.gro
│   ├── em.log
│   ├── em.tpr
│   ├── em.trr
│   └── mdout.mdp
├── md.mdp
├── md_0_1.cpt
├── md_0_1.edr
├── md_0_1.gro
├── md_0_1.log
├── md_0_1.tpr
├── md_0_1.trr
├── md_0_1.xtc
├── md_0_1_fix.xtc
├── mdout.mdp
├── minim
│   ├── #topol.top.1#
│   ├── #topol.top.2#
│   ├── TALE.gro
│   ├── TALE_newbox.gro
│   ├── TALE_solv.gro
│   ├── TALE_solv_ions.gro
│   ├── ions.mdp
│   ├── ions.tpr
│   ├── mdout.mdp
│   └── minim.mdp
├── npt
│   ├── npt.cpt
│   ├── npt.edr
│   ├── npt.gro
│   ├── npt.log
│   ├── npt.mdp
│   ├── npt.tpr
│   ├── npt.trr
│   ├── posre.itp
│   └── topol.top
└── nvt
    ├── mdout.mdp
    ├── nvt.cpt
    ├── nvt.edr
    ├── nvt.gro
    ├── nvt.log
    ├── nvt.mdp
    ├── nvt.tpr
    └── nvt.trr
gmx.sh
log
└── TALE.pdb
mdp
├── ions.mdp
├── md.mdp
├── minim.mdp
├── npt.mdp
└── nvt.mdp
pdb
rmsd
└── TALE_rmsd.csv
