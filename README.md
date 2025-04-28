# General Goals
The two goals of this project are to test existing models which have Assamese data using TSE (Targeted Syntactic Evaluation) for features of Assamese that are more typologically unique, such as phrasal movement for definiteness marking and classifier selection, to determine the effectiveness of existing models in representing Assamese. After that, we will adapt a pretrained Bengali model using some Assamese data to see how well such a model might perform, as Assamese and Bengali share a lot of vocabulary and grammatical structures, and while vocally they are mutually unintelligible, in writing they can look very similar especially as they use the same script.

The repository tests three models currently, AxomiyaBERTa, XLM-R, and IndicBERT (all cited within the runnable notebook), accessed using the HuggingFace API. 

# How to Use
The file "bertlike_models.ipynb" is the main runnable file, which tests sentence pairs across three different existing models and shows their performances. The metric is (currently) to calculate the surprisal of a sentence pair, concatenated into one document, where the first sentence is a context, and the second sentence is a continuation. For example, the context "A boy and a girl walked into the classroom." has two continuations given: ["A boy sat down.", "The boy sat down."]. We therefore form two sentence pairs, #"A boy and a girl walked into the classroom. A boy sat down.", and "A boy and a girl walked into the classroom. The boy sat down.". In English, only the second pair felicitous, while the first one is infelicitous. We track how many times the model's surprisal shows a minimal surprisal value for the felicitous sentence pair (as compared to the infelicitous one) and report that in aggregate for the model across all documents.

(Currently, there are only a few documents for testing purposes; more will be made later)

WIP: The file "bengali_model_adaptation.ipynb" is the (unfinished) file where we will retrain a pretrained Bengali/Bangla model, but adapted to Assamese. We will then use the same surprisal evaluation as for the first task to compare it to the existing models. The "assamese_corpus" folder is intended to house the corpus I use to train it.

# Files and Folders
The files "bertlike_models.ipynb" and "bengali_model_adaptation.ipynb" are the main runnable files, as explained above.

The folder "test_sentences" contains files with testing sentences. The sentences are formatted as follows:<br>
```
(Context),(Translation)
    (Sentence),(Translation),(1 for preferred,0 for not preferred)
    (Sentence),(Translation),(1 for preferred,0 for not preferred)
    ...
```

The folder "access_items" holds huggingface keys and api keys. Github does not allow secrets, so please put a file called "hg_token.txt" inside the folder "access_items" containing a HuggingFace token which gives you permission to use all of the models listed here (most importantly, AxomiyaBERTa requires special access that is granted by simply going to the site and accepting a license agreement).

The folder "licenses" contains licenses for libraries used.

The folder "wip_or_not_used" is a folder for things that are still being figured out and should NOT be run.
